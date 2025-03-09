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
