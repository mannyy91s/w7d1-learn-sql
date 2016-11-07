Explorer Mode:
Questions:
Q.)How many users are there?
A.) 50
Command Used: select (x) from users;

Q.)What are the 5 most expensive items?
A.)9984        Small Cotton Gloves
9859        Small Wooden Comput
9790        Awesome Granite Pan
9390        Sleek Wooden Hat   
9341        Ergonomic Steel Car
Command Used: select items.price, items.title from items order by price desc;

Q.)What's the cheapest book? (Does that change for "category is exactly 'book'" versus "category contains 'book'"?)
A.) Cheapest books for category that is exactly 'book'
1496        Books                       Ergonomic Granite C
3056        Books                       Practical Plastic H
8904        Books                       Fantastic Rubber Sh
9246        Books                       Fantastic Steel Cha

Cheapest books for category that contains 'book'
2377        Books, Toys & Tools         Incredible Granite
6720        Toys & Books                Fantastic Rubber Sh
9341        Books & Outdoors            Ergonomic Steel Car
9790        Toys & Books                Awesome Granite Pan
Command Used: select items.price, items.category, items.title from items order by price desc;

Q.)Who lives at "6439 Zetta Hills, Willmouth, WY"? Do they have another address?
A.) User id: 40 lives there. They also have another address : 54369 Wolff Forg, Lake Bryon, CA  31587
Command Used: select addresses.street, addresses.user_id from addresses where street like '%Zetta Hills%';
Command Used: select addresses.user_id, addresses.street, addresses.city, addresses.state, addresses.zip from addresses where user_id like '%40%';

Q.)Correct Virginie Mitchell's address to "New York, NY, 10108".
A.) I Found out the id for virginie first then updated her address.
Command Used: select users.id, users.first_name, users.last_name from users where first_name like '%virginie%';
Command Used:  select users.id, users.first_name, users.last_name from users inner join addresses on users.id=addresses.user_id;
Command Used: update addresses set city='New York', state='NY', zip='10108' where addresses.id=41;

Q.)How much would it cost to buy one of each tool?
A.) category    price       total     
----------  ----------  ----------
Tools       1107        467488    
Tools       5437        467488    
Tools       839         467488  
sum total for category that just contains tools = 467488.
Command Used: select items.category, items.price,(select sum(items.price) from items) total from items where items.category='Tools';

category               price       total     
---------------------  ----------  ----------
Beauty, Shoes & Tools  7476        467488    
Industrial & Tools     2851        467488    
Tools                  1107        467488    
Garden, Toys & Tools   798         467488    
Tools, Garden & Movie  3335        467488    
Tools, Clothing & Toy  615         467488    
Tools, Jewelery & Ind  7606        467488    
Tools, Garden & Games  1913        467488    
Tools & Computers      2768        467488    
Sports & Tools         3160        467488    
Tools                  5437        467488    
Games, Sports & Tools  5210        467488    
Tools                  839         467488    
Books, Toys & Tools    2377        467488    
Tools & Kids           985         467488
Command Used: select items.category, items.price,(select sum(items.price) from items) total from items where items.category like '%tools%';

Q.)How many total items did we sell?
A.)quantity    total     
----------  ----------
2           2125
Command Used: select orders.quantity, sum(orders.quantity) total from orders;

Q.)How much was spent on books?
A.)Books	3056	420566
Command Used: select items.category, items.price, sum(items.price*orders.quantity) from items INNER JOIN orders on orders.item_id=items.id where items.category='Books';

Q.)Simulate buying an item by inserting a User for yourself and an Order for that User.
A.)id          first_name  last_name   email                     
----------  ----------  ----------  --------------------------   
51          manny       singh       manny@gmail.com           
Command Used: insert into users values(51, 'manny','singh','manny@gmail.com');

id          user_id     item_id     quantity    created_at                
378         51          1337        1           2016-11-07 20:10:15  
Command Used: insert into orders values(378,51,1337,1, datetime());
