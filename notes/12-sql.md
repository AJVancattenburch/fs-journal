# SQL

## **Day 1**

### *Rebuilding Post-It*

* Steps
  + Create a new project
  + Make sure you add your necessary auth settings in your `appsettings.development.json file`
  + Example:
  ```json
  "CONNECTION_STRING": "Server=localhost;Database=;User Id=;Password=;"
  ```
  + **REMEMEBER:** The `FOREIGN KEY IS NOT` a property of the model. It is a simply a `relationship between two tables.`
  + Execute your table in your `dbSetup.sql file`
  + Example:
  ```sql
  CREATE TABLE IF NOT EXISTS "Notes" (
    Id SERIAL PRIMARY KEY,
    Title VARCHAR(255) NOT NULL,
    Content VARCHAR(255) NOT NULL,
    UpdatedAt DATETIME DEFAULT ON UPDATE CURRENT_TIMESTAMP COMMENT 'Last updated time',
  );
  ```

  + First thing you want to do to save the information to your database is to `create a table in your dbSetup.sql file for your albums`
  + Example:
  ```sql
  CREATE TABLE IF NOT EXISTS "Albums" (
    id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    category VARCHAR(255) NOT NULL DEFAULT 'misc',
    coverImg VARCHAR(500) NOT NULL,
    archived BOOLEAN NOT NULL DEFAULT false,
    creatorId VARCHAR(255) NOT NULL,
    createdAt DATETIME DEFAULT CURRENT_TIMESTAMP COMMENT 'Time created',
    updatedAt DATETIME DEFAULT ON UPDATE CURRENT_TIMESTAMP COMMENT 'Last updated time',

    FOREIGN KEY (creatorId) REFERENCES accounts(id)
    //NOTE - ADDING A HOOK
    ON ArchiveAlbum CASCADE
    //NOTE - 'ArchiveAlbum CASCADE' WILL ArchiveAlbum ALL THE ALBUMS ASSOCIATED WITH THE ACCOUNT. ESSENTIALLY SAYING 'IF I ArchiveAlbum MY ACCOUNT, EVERYTHING I HAVE CREATED WILL BE ArchiveAlbumD AS WELL'
  ) default charset utf8 COMMENT '';

  INSERT INTO albums
  (title, category, coverImg, archived, creatorId)
  VALUES
  ('Retro Pugs', 'Pugs', 'https://images.unsplash.com/photoexample', false, '34985sdf98asd0a9s8d7f');

  INSERT INTO albums
  (title, category, coverImg, archived, creatorId)
  VALUES
  ('Music', 'Aesthetics', 'https://images.unsplash.com/photoexample', false, '34985sdf98asd0a9s834rf');

  INSERT INTO albums
  (title, category, coverImg, archived, creatorId)
  VALUES
  ('Fast Cars', 'games', 'https://images.unsplash.com/photoexample', false, '34985sdf98asd0a9s8d7f');

  ArchiveAlbum FROM albums WHERE id = 1;
  
  ArchiveAlbum FROM albums WHERE id = '645d2b2a1b1a4b8a8ba';

  --//REVIEW - THE BELOW EXAMPLE EFFECTIVELY DEMONSTRATES HOW YOU WOULD JOIN TWO TABLES TOGETHER DISPLAYING THE **INFO FOR THE ALBUMS AND THE ACCOUNTS WITHOUT GETTING THE INFO FOR THE CREATOR**//
  SELECT * 
  FROM albums;
  JOIN accounts ON albums.creatorId = accounts.id;
  WHERE accounts.id = '90q384ruq0n348345qv34';

  --//REVIEW - THE BELOW EXAMPLE EFFECTIVELY DEMONSTRATES HOW YOU WOULD **JOIN TWO TABLES TOGETHER DISPLAYING THE INFO FOR THE ALBUMS AND THE ACCOUNTS**//
  SELECT  
    alb.*,
    creator.*,
  FROM albums alb
  JOIN accounts creator ON alb.creatorId = creator.id;
  WHERE creator.id = '90q384ruq0n348345qv34';

  --//REVIEW - THE BELOW EXAMPLE EFFECTIVELY DEMONSTRATES HOW YOU WOULD **JOIN TWO TABLES TOGETHER DISPLAYING THE INFO FOR THE ALBUMS TITLE AND NAME**//
  SELECT
    title, name 
  FROM albums
  JOIN accounts ON albums.creatorId = accounts.id;
  WHERE accounts.id = '90q384ruq0n348345qv34';
  ```

  <br> <br>

  + Start by building out your `model, controller, repository, and service` for your table.

  <br> <br>

  + Creating the `model for your table`
  + Example:
  ```cs
  public class Album
  {
    public int Id { get; set; }
    public string Title { get; set; }
    public string Category { get; set; }
    public string CoverImg { get; set; }
    public bool Archived { get; set; }
    public string CreatorId { get; set; }
    public Account Creator { get; set; }
    public DateTime CreatedAt { get; set; }
    public DateTime UpdatedAt { get; set; }
  }
  ```
  
  + Creating the `controller for your table`
  + Example:
  ```cs
  [ApiController]
  [Route("api/[controller]")]

  public class AlbumsController : ControllerBase
  {
    private readonly AlbumsService _albumsservice;

    public AlbumsController(AlbumsService albumsService)
    {
      _albumsService = albumsService;
    }

    [HttpPost]
    [Authorize]
    //NOTE - **ASYNC AND AWAIT** CAN NOW BE USED FOR THE BELOW METHOD IN ORDER TO VERIFY THE USER//
    //NOTE - ANY TIME YOU ARE USING **ASYNC AND AWAIT** YOU MUST USE THE **TASK** CLASS//
    public async Task<ActionResult<Album>> CreateAlbum([FromBody] Album albumData)
    {
      try
      {
        //NOTE - WE **AWAIT** IN THE LINE BELOW SO WE CAN **VERIFY THE USER** FROM AUTH0//
        Account userInfo = await auth.GetUserInfoAsync<Account>(HttpContext);
        //NOTE - THIS EXAMPLE BELOW **ATTACHES THE DATA FROM THE BODY**//
        albumData.CreatorId = userInfo.Id;
        Album album = _albumsService.CreateAlbum(albumData);
        return Ok(album);
      }
      catch (Exception e)
      {
        return BadRequest(e.Message);
      }
    }

    [HttpGet]
    public ActionResult<List<Album>> GetAllAlbums()
    {
      try
      {
        List<Album> albums = _albumsService.GetAllAlbums();
        return Ok(albums);
      }
      catch (Exception e)
      {
        return BadRequest(e.Message);
      }
    }

    [HttpGet("{albumId}")]
    public ActionResult<Album> GetById(int albumId)
    {
      try
      {
        Album album = _repo.GetById(albumId);
        return Ok(album);
      }
      catch (Exception e)
      {
        return BadRequest(e.Message);
      }
    }

    [HttpPut("{albumId}")]
    public ActionResult<Album> Edit([FromBody] Album updateAlbum, int id)
    {
      try
      {
        updateAlbum.Id = id;
        return Ok(_albumService.Edit(updateAlbum));
      }
      catch (Exception e)
      {
        return BadRequest(e.Message);
      }
    }

    [HttpDelete("{albumId}")]
    [Authorize]
    public async ActionResult<Album> ArchiveAlbum(int id)
    {
      try
      {
        Account userInfo = await auth.GetUserInfoAsync<Account>(HttpContext);
        Album album = _albumsService.ArchiveAlbum(id, userInfo.Id);
      }
      catch (Exception e)
      {
        return BadRequest(e.Message);
      }
    }
  }
  ```


  + Creating the `repository for your table`
  + Example:
  ```cs
  public class AlbumsRepository
  {
    private readonly IDbConnection _db;

    public AlbumsRepository(IDbConnection db)
    {
      _db = db;
    }

    internal IEnumerable<Album> GetAllAlbums()
    {
      string sql = @"
      SELECT 
        alb.*,
        creator.*
      FROM albums alb
      JOIN accounts creator ON alb.creatorId = creator.id;
      ";

      List<Album> = _db.Query<Album, Account, Album>(sql, (album, creator) =>
      {
        album.Creator = creator;
        return album;
      }).ToList();
      return albums;
    }

    internal Album GetById(int albumId)
    {
      string sql = "SELECT * FROM albums WHERE albumId = @albumId;";
      Album album = _db.Query<Album> (new { id }).FirstOrDefault();
      return album;
    }

    internal Album CreateAlbum(Album albumData)
    {
      string sql = @"
      INSERT INTO albums
      (title, category, coverImg, archived, creatorId)
      VALUES
      (@Title, @Category, @CoverImg, @Archived, @CreatorId);
      SELECT  
        alb.*,
        creator.*,
      FROM albums alb
      JOIN accounts creator ON alb.creatorId = creator.id;
      WHERE alb.id = LAST_INSERT_ID();";
      int id = _db.ExecuteScalar<int>(sql, albumData);
      albumData.Id = id;
      return albumData;
    }

    internal void UpdateAlbum(Album album)
    {
      string sql = @"
      UPDATE albums
      SET
        title = @title,
        category = @category,
        coverImg = @coverImg,
        archived = @archived
      WHERE alb.id = @albumId;";
      _db.Execute(sql, album);
    }

    internal void ArchiveAlbum(int albumId, string userId)
    {
      Album album = GetById(albumId);
      if (album.CreatorId != userId)
      {
        throw new Exception("This is not your album!");
      }
      album.Archived = !album.Archived;
      _repo.UpdateAlbum(album);
      string sql = "ArchiveAlbum FROM albums WHERE id = @id LIMIT 1;";
      _db.Execute(sql, new { albumId });
    }
  }
  ```

  + Creating the `service for your table`
  + Example:
  ```cs
  public class AlbumsService
  {
    private readonly AlbumsRepository _repo;

    public AlbumsService(AlbumsRepository repo)
    {
      _repo = repo;
    }

    internal Album CreateAlbum(Album albumData)
    {
      string sql = @"
      INSERT INTO albums
      (title, category, coverImg, archived, creatorId)
      VALUES
      (@title, @category, @coverImg, @archived, @creatorId;)
      SELECT * FROM albums WHERE id = LAST_INSERT_ID();";
      //REVIEW - RETURN =========> ⬇️
      //FIRST SELECT ==========> ⬇️
      //SECOND SELECT =========> ⬇️
      // ===> ⬇️ 
      //RETURN =========> ⤵️
      Album album = _db.Query<Album, Account, Album>(sql, (album, account) =>
      {
        //REVIEW - FIRST ==> SECOND
        album.Creator = account;
        return album; //REVIEW - RETURN (ALBUM)

      }, albumData).FirstOrDefault();
          return album;
    }

    internal List<Album> GetAllAlbums()
    {
      return _repo.GetAllAlbums();
    }

    internal Album UpdateAlbum(Album updateAlbum)
    {
      Album original = GetById(updateAlbum.Id);
      if (original == null)
      {
        throw new Exception("Invalid Id");
      }
      original.Title = updateAlbum.Title != null ? updateAlbum.Title : original.Title;
      original.Category = updateAlbum.Category != null ? updateAlbum.Category : original.Category;
      original.CoverImg = updateAlbum.CoverImg != null ? updateAlbum.CoverImg : original.CoverImg;
      original.Archived = updateAlbum.Archived != null ? updateAlbum.Archived : original.Archived;
      return _repo.UpdateAlbum(original);
    }
  }
  ```

  + Add your `service and repo to your startup.cs file`
  + Example:
  ```cs
  services.AddScoped<AlbumsService>();
  services.AddScoped<AlbumsRepository>();
  ```

## **Day 2**

### *Rebuilding Post-It - Pictures*

* Steps
  + Make sure you are connected to your database by running your `dbSetup.sql file`
  + You should see a notification at the bottom of your activity bar in vscode
  + Create your `pictures` table in your `dbSetup.sql file`
  + Example:
  ```sql
  CREATE TABLE IF NOT EXISTS pictures (
    Id SERIAL PRIMARY KEY COMMENT 'Primary Key',
    imgUrl VARCHAR(500) NOT NULL,
    CreatorId VARCHAR(255) NOT NULL,
    albumId INT NOT NULL,
    CreatedAt DATETIME DEFAULT CURRENT_TIMESTAMP COMMENT 'Time created',
    UpdatedAt DATETIME DEFAULT ON UPDATE CURRENT_TIMESTAMP COMMENT 'Last updated time',

    FOREIGN KEY (AlbumId) REFERENCES albums(id) ON DELETE CASCADE,
    FOREIGN KEY (CreatorId) REFERENCES accounts(id) ON DELETE CASCADE
  ) default charset utf8 COMMENT '';
  ```

  + Now you can continue on to creating your model for your pictures table.
  + Example:
  ```cs
  namespace PostItSharp.Models;

  public class Picture
  {
    public int Id { get; set; }
    public string ImgUrl { get; set; }
    public string CreatorId { get; set; }
    public int AlbumId { get; set; }
    public Account Creator { get; set;}
    public DateTime CreatedAt { get; set; }
    public DateTime UpdatedAt { get; set; }
  }
  ```

  + This time we will create our repository first for `pictures` then work our way into the `controller` and `service` layer.
  + Building the repository for `pictures`
  + Example:
  ```cs
  namespace PostItSharp.Repositories;

  public class PicturesRepository
  {
    private readonly PicturesRepository _repo;

    public PicturesRepository(PicturesRepository repo)
    {
      _repo = repo;
    }
  }

  ```

  + Building the `service layer` for `pictures`
  + Example:
  ```cs
  namespace postitsharp.Services;

  public class PicturesService
  {
    private readonly PicturesRepository _repo;

    public PicturesService(PicturesRepository repo)
    {
      _repo = repo;
    }
  } 
  ```

  + Now you can create your first `post` method starting in your controller.
  + Example:
  ```cs
  namespace PostItSharp.Controllers;

  [ApiController]
  [Route("api/[controller]")]

  public class PicturesController : ControllerBase
  {
    private readonly PicturesService _picturesService;

    private readonly Auth0Provider _auth;

    public PicturesController(PicturesService picturesService)
    {
      _picturesService = picturesService;
    }

    [HttpPost]
    [Authorize]

    public async Task<ActionResult<Picture>> CreatePicture([FromBody] Picture pictureData)
    {
      try
      {
        Account userInfo = await _auth.GetUserInfoAsync<Account>(HttpContext);
        pictureData.CreatorId = userInfo.Id;
        Picture picture = _picturesService.CreatePicture(pictureData);
        return Ok(picture);
      }
      catch (Exception e)
      {
        return BadRequest(e.Message);
      }
    }
  }
  ```

  + How move onto your `pictures repository layer` to continue building out your post request.
  + Example:
  ```cs
    internal Picture CreatePicture(Picture pictureData)
    {
      string sql = @"
      INSERT INTO pictures
        (imgUrl, creatorId, albumId)
      VALUES
        (@imgUrl, @creatorId, @albumId);
      SELECT
        pic.*,
        acc.*
      FROM pictures
      JOIN accounts acc ON acc.id = pic.creatorId
      WHERE pic.id = LAST_INSERT_ID();
      ";
      Picture picture = _db.Query<Picture, Account, Picture>(sql, (picture, account) =>
      {
        picture.Creator = account;
        return picture;
      }, pictureData).FirstOrDefault();
      return picture;
    }
  ```

  + Be sure you add your `service and repo` to your `startup.cs file`
  + Example:
  ```cs
  services.AddScoped<PicturesService>();
  services.AddScoped<PicturesRepository>();
  ```

  + Now you can `test your post request in postman` to make sure everything is working properly.
  + After that step, note that you do not need to build a function through your `service and repo` for your `get all pictures` method. You only need to grab the `id` of the `album` you are trying to get the pictures for in your album controller and service.
  + Example:
  ```cs
  [HttpGet("{albumId}/pictures")]

  public ActionResult<List<Picture>> GetPicturesByAlbumId(int albumId)
  {
    try
    {
      List<Picture> pictures = _picturesService.GetPicturesByAlbumId(albumId);
      return Ok(pictures);
    }
    catch (Exception e)
    {
      return BadRequest(e.Message);
    }
  }
  ```
  + Next, you can build out your `get pictures by album id` method in your `pictures service layer`
  + Example:
  ```cs
  internal List<Picture> GetPicturesByAlbumId(int albumId)
  {
    string sql = @"
    SELECT
      pic.*,
      acc.*
    FROM pictures pic
    JOIN accounts acc ON acc.id = pic.creatorId
    WHERE pic.albumId = @albumId;
    ";
    return _db.Query<Picture, Account, Picture>(sql, (picture, account) =>
    {
      picture.Creator = account;
      return picture;
    }, new { albumId }, splitOn: "id").ToList();
  }
  ```
  + Now you can `test your get request in postman` to make sure everything is working properly.

  + Once you're passing the test, you can build out your delete method in your `pictures controller`
  + Example:
  ```cs
  [HttpDelete("{pictureId}")]
  [Authorize]

  public async Task<ActionResult<Picture>> DeletePicture(int pictureId)
  {
    try
    {
      Account userInfo = await _auth.GetUserInfoAsync<Account>(HttpContext);
      _picturesService.DeletePicture(pictureId, userInfo.Id);
      return Ok("Picture Deleted!");
    }
    catch (Exception e)
    {
      return BadRequest(e.Message);
    }
  }
  ```

  + Now you can build out your `delete picture` method in your `pictures service layer`
  + Example:
  ```cs
  internal void DeletePicture(int pictureId, string userId)
  {
    Picture picture = GetById(pictureId);
    if (picture.CreatorId != userId)
    {
      throw new Exception("This is not your picture!");
    }
    string sql = "DELETE FROM pictures WHERE id = @pictureId LIMIT 1;";
    _db.Execute(sql, new { pictureId });
  }
  ```

  + Finally, you can build your delete method in your `pictures repository layer`
  + Example:
  ```cs
  internal void DeletePicture(int pictureId)
  {
    string sql = @"
    DELETE FROM pictures
    WHERE id = @pictureId LIMIT 1
    ;";
    int rows = _db.Execute(sql, new { pictureId });
  }
  ```
* ***HOW TO USE MYSQL WORKBENCH***
  + D
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 
  + 



















1. Ordered list
2. Nested
   1. 
   2. 
   3. 
   4. 
   5. 
   6. 
   7. 
   8. 
   9. 
   10. 
   11. 
   12. 
   13. 
   14. 
   15. 
   16. 
   17. 
   18. 
   19. 
   20.
   21. 
   22. 
   23. 
   24. 
   25. 
   26. 
   27. 
   28. 
   29. 
   30.
   31. 
   2. 
   3. 
   4. 
   5. 
   6. 
   7. 
   8. 
   9. 
   40.
   41. 
   2. 
   3. 
   4. 
   5. 
   6. 
   7. 
   8. 
   9. 
   50.
   51. 
   2. 
   3. 
   4. 
   5. 
   6. 
   7. 
   8. 
   9. 
   60.