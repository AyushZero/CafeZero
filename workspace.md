# SQL Schema

Location(LocationID, City, Employees, Address)
Customer(CustomerID, LoyaltyID, PhoneNo, Name, Password, Email)
Employee(EmployeeID, Role, Salary, PhoneNo, Name, Password, Email)
Admin(AdminID, Name, Email, Password, PhoneNo)
Menu_Item(MenuItemID, Category, Price, Name, Description)
Inventory(SupplyID, LastRestock, Inventory, Code, LocationID)
Orders(OrderID, CustomerID, LocationID, Amount, Status, OrderDateTime)
Order_Item(OrderItemID, CustomerItemID, OrderID, MenuItemID, Quantity, Price)
Reservation(ReservationID, CustomerID, LocationID, ReservationDate, ReservationTime, Status)
Schedule(EmployeeID, ShiftID, LocationID, ShiftTimings)
Loyalty(LoyaltyID, CustomerID, PointsRedeemed, PointsEarned)
Coffee_Supply(SupplyID, LocationID, RoastDate, Quantity)

# **Primary Command**  
CREATE DATABASE IF NOT EXISTS Cafe;  
USE Cafe;

DROP TABLE IF EXISTS Coffee\_Supply;  
DROP TABLE IF EXISTS Loyalty;  
DROP TABLE IF EXISTS Schedule;  
DROP TABLE IF EXISTS Reservation;  
DROP TABLE IF EXISTS Order\_Item;  
DROP TABLE IF EXISTS Orders;  
DROP TABLE IF EXISTS Inventory;  
DROP TABLE IF EXISTS Menu\_Item;  
DROP TABLE IF EXISTS Admin;  
DROP TABLE IF EXISTS Employee;  
DROP TABLE IF EXISTS Customer;  
DROP TABLE IF EXISTS Location;

CREATE TABLE Location (  
    LocationID INT PRIMARY KEY,  
    City VARCHAR(100),  
    Employees INT,  
    Address VARCHAR(255)  
);

CREATE TABLE Customer (  
    CustomerID INT PRIMARY KEY,  
    LoyaltyID INT,  
    PhoneNo VARCHAR(20),  
    Name VARCHAR(100),  
    Password VARCHAR(100),  
    Email VARCHAR(100)  
);

CREATE TABLE Employee (  
    EmployeeID INT PRIMARY KEY,  
    Role VARCHAR(50),  
    Salary DECIMAL(10,2),  
    PhoneNo VARCHAR(20),  
    Name VARCHAR(100),  
    Password VARCHAR(100),  
    Email VARCHAR(100)  
);

CREATE TABLE Admin (  
    AdminID INT PRIMARY KEY,  
    Name VARCHAR(100),  
    Email VARCHAR(100),  
    Password VARCHAR(100),  
    PhoneNo VARCHAR(20)  
);

CREATE TABLE Menu\_Item (  
    MenuItemID INT PRIMARY KEY,  
    Category VARCHAR(50),  
    Price DECIMAL(10,2),  
    Name VARCHAR(100),  
    Description TEXT  
);

CREATE TABLE Inventory (  
    SupplyID INT PRIMARY KEY,  
    LastRestock DATE,  
    Inventory INT,  
    Code VARCHAR(50),  
    LocationID INT,  
    FOREIGN KEY (LocationID) REFERENCES Location(LocationID)  
);

CREATE TABLE Orders (  
    OrderID INT PRIMARY KEY,  
    CustomerID INT,  
    LocationID INT,  
    Amount DECIMAL(10,2),  
    Status VARCHAR(50),  
    OrderDateTime DATETIME,  
    FOREIGN KEY (CustomerID) REFERENCES Customer(CustomerID),  
    FOREIGN KEY (LocationID) REFERENCES Location(LocationID)  
);

CREATE TABLE Order\_Item (  
    OrderItemID INT PRIMARY KEY,  
    CustomerItemID INT,  
    OrderID INT,  
    MenuItemID INT,  
    Quantity INT,  
    Price DECIMAL(10,2),  
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID),  
    FOREIGN KEY (MenuItemID) REFERENCES Menu\_Item(MenuItemID)  
);

CREATE TABLE Reservation (  
    ReservationID INT PRIMARY KEY,  
    CustomerID INT,  
    LocationID INT,  
    ReservationDate DATE,  
    ReservationTime TIME,  
    Status VARCHAR(50),  
    FOREIGN KEY (CustomerID) REFERENCES Customer(CustomerID),  
    FOREIGN KEY (LocationID) REFERENCES Location(LocationID)  
);

CREATE TABLE Schedule (  
    EmployeeID INT,  
    ShiftID INT,  
    LocationID INT,  
    ShiftTimings VARCHAR(100),  
    PRIMARY KEY (EmployeeID, ShiftID),  
    FOREIGN KEY (EmployeeID) REFERENCES Employee(EmployeeID),  
    FOREIGN KEY (LocationID) REFERENCES Location(LocationID)  
);

CREATE TABLE Loyalty (  
    LoyaltyID INT PRIMARY KEY,  
    CustomerID INT,  
    PointsRedeemed INT,  
    PointsEarned INT,  
    FOREIGN KEY (CustomerID) REFERENCES Customer(CustomerID)  
);

CREATE TABLE Coffee\_Supply (  
    SupplyID INT,  
    LocationID INT,  
    RoastDate DATE,  
    Quantity INT,  
    PRIMARY KEY (SupplyID, LocationID, RoastDate),  
    FOREIGN KEY (SupplyID) REFERENCES Inventory(SupplyID),  
    FOREIGN KEY (LocationID) REFERENCES Location(LocationID)  
);