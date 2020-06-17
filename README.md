##create table
--------------------------------------------------
SET SQL_MODE = "NO_AUTO_VALUE_ON_ZERO";
SET time_zone = "+00:00";
CREATE TABLE users
(
  id INT(20) PRIMARY KEY AUTO_INCREMENT,
  email VARCHAR(50),
  password VARCHAR(50),
  role VARCHAR(50),
  created_at TIMESTAMP,
  updated_at TIMESTAMP
);

CREATE TABLE categories
(
  id INT(20) PRIMARY KEY AUTO_INCREMENT,
  name VARCHAR(50),
  created_at TIMESTAMP,
  updated_at TIMESTAMP
);

CREATE TABLE photos
(
  id INT(20) PRIMARY KEY AUTO_INCREMENT,
  title VARCHAR(100),
  category_id INT(20),
  image VARCHAR(100),
  created_at TIMESTAMP,
  updated_at TIMESTAMP,
  FOREIGN KEY (category_id) REFERENCES categories (id)
);
CREATE TABLE tags
(
id INT(20) PRIMARY KEY AUTO_INCREMENT,
name VARCHAR(50),
created_at TIMESTAMP,
updated_at TIMESTAMP
);
CREATE TABLE taggable
(
  tag_id INT(20) ,
  photo_id INT(20),
  created_at TIMESTAMP,
  updated_at TIMESTAMP,
   PRIMARY KEY (photo_id, tag_id),
  FOREIGN KEY (photo_id) REFERENCES photos(id),
  FOREIGN KEY (tag_id) REFERENCES tags(id)
);

CREATE TABLE photo_descriptions
(
  photo_id INT(20),
  content VARCHAR(100),
  created_at TIMESTAMP,
  updated_at TIMESTAMP,
  FOREIGN KEY (photo_id) REFERENCES photos(id)
);
##Insert data
INSERT INTO categories(name) VALUES ('Hai huoc'),
);
INSERT INTO tags(name) VALUES ('Meo con'),
                             ;
INSERT INTO users(email, password, role) VALUES ('yeuho@gmail.com','hothiyeu','admin'),
                                               ;
INSERT INTO photos(title, category_id, image) VALUES ('hinh anh duoi nuoc',1,'haihuoc.png'),                                                ;
INSERT INTO photo_descriptions(photo_id,content) VALUES (1,'kham pha nhung noi ban chua tung den');
INSERT INTO taggable(tag_id,photo_id) VALUES(1,2),
                                          (2,1),
                                          (1,1),
                                          (2,2);
##Query
SELECT p.title, ca.name, pd.content
FROM photos as p
JOIN categories as ca
ON p.category_id = ca.id
JOIN photo_descriptions as pd ON pd.photo_id = p.id
----------
SELECT p.id, p.title, tags.id, GROUP_CONCAT(tags.id,tags.name) FROM photos as p LEFT JOIN taggable as tg ON p.id = tg.photo_id LEFT JOIN tags ON tg.tag_id = tags.id GROUP BY p.id;