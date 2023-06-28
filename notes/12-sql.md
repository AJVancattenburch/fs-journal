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