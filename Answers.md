
Questions

1. Explain the relationship between the "Product" and "Product_Category" entities from the above diagram.

Answer -1 

Product:

Attributes: id, name, desc, Sku, category_id, Inventory_id, Price, diacount_id, Created_id, modified_at, delete_at.
The "category_id" attribute serves as a foreign key referencing the primary key "id" in the "product_category" table.
This relationship indicates that each product is associated with a specific product category defined in the "product_category" table.
Product_Category:

Attributes: id, name, desc, created_at, modified_at, deleted_at.
The "id" attribute serves as the primary key of the "product_category" table.


Questions 

2. How could you ensure that each product in the "Product" table has a valid category assigned to it?


Answer -2

ALTER TABLE Product
ADD CONSTRAINT fk_product_category
FOREIGN KEY (category_id)
REFERENCES product_category(id);



Questions 

3. Create schema in any Database script or any ORM (Object Relational Mapping).

Answer -3

--------Schema Of ORM-------------

CREATE TABLE Product (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255),
    description TEXT,
    Sku VARCHAR(50),
    category_id INT,
    Inventory_id INT,
    Price DECIMAL(10, 2),
    discount_id INT,
    Created_id TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    modified_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    delete_at TIMESTAMP,
    FOREIGN KEY (category_id) REFERENCES product_category(id),
    FOREIGN KEY (Inventory_id) REFERENCES product_inventory(id),
    FOREIGN KEY (discount_id) REFERENCES discount(id)
);

-- Create Product Category table
CREATE TABLE product_category (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255),
    description TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    modified_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    deleted_at TIMESTAMP
);

-- Create Product Inventory table
CREATE TABLE product_inventory (
    id INT AUTO_INCREMENT PRIMARY KEY,
    quantity INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    modified_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    deleted_at TIMESTAMP
);

-- Create Discount table
CREATE TABLE discount (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255),
    description TEXT,
    discount_percent DECIMAL(5, 2),
    active BOOLEAN,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    modified_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    deleted_at TIMESTAMP
);

