Chương 1: PortgreSQL
Tạo cơ sở dữ liệu
CREATE DATABASE bat_dong_san_db;
Kết nối vào cơ sở dữ liệu
\c bat_dong_san_db
CREATE TABLE
Ví dụ:
CREATE TABLE cars (
  brand VARCHAR(255),
  model VARCHAR(255),
  year INT
);
ADD COLUMN
ALTER TABLE cars
ADD color VARCHAR(255);
UPDATE
UPDATE cars
SET color = 'red'
WHERE brand = 'Volvo';
INSERT INTO 
INSERT INTO cars (brand, model, year)
VALUES ('Ford', 'Mustang', 1964);