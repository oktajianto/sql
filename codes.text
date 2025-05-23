///buat penghubung antar database kolom isi sama

DELIMITER //

CREATE TRIGGER after_update_product
AFTER UPDATE ON databaseallitem
FOR EACH ROW
BEGIN
  -- Update kolom item
  UPDATE tes0
  SET item = NEW.product
  WHERE item = OLD.product; 
 
  -- Update kolom keterangan
  UPDATE tes0
  SET keterangan = REPLACE(keterangan, OLD.product, NEW.product)
  WHERE keterangan LIKE CONCAT('%', OLD.product, '%');
END;
//

DELIMITER ;

///versi efisien
DELIMITER //

CREATE TRIGGER after_update_product
AFTER UPDATE ON databaseallitem
FOR EACH ROW
BEGIN
  UPDATE tes0
  SET 
    item = CASE WHEN item = OLD.product THEN NEW.product ELSE item END,
    keterangan = CASE 
      WHEN keterangan LIKE CONCAT('%', OLD.product, '%')
      THEN REPLACE(keterangan, OLD.product, NEW.product)
      ELSE keterangan
    END
  WHERE item = OLD.product OR keterangan LIKE CONCAT('%', OLD.product, '%');
END;
//

DELIMITER ;

///

