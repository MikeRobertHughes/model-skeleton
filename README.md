##Normal Mode

1.  How many users are there?
    User.count => 50

2.  What are the 5 most expensive items?
    Item.limit(5).order('price desc')

3.  What’s the cheapest book?
    Item.where("category LIKE ?", "%book%").order(price: 'ASC').limit(1)

4.  Who lives at “6439 Zetta Hills, Willmouth, WY”? Do they have another address?
    Address.where(street: '6439 Zetta Hills') => user_id = 40
    Address.where(user_id: 40)

5.  Correct Virginie Mitchell’s address to “New York, NY, 10108”.
    User.where(first_name: 'Virginie', last_name: 'Mitchell') => user_id = 39
    Address.where(user_id: 39).update_all(city: 'New York', state: 'NY', zip: 10108) => 2

6.  How much would it cost to buy one of each tool?
    Item.where("category LIKE ?", "%tool%").sum('price') => 46477

7.  How many total items did we sell?
    Order.sum('quantity') => 2125

8.  How much was spent on books?
    Order.joins("INNER JOIN items ON orders.item_id = items.id").where("category LIKE ?", "%book%").sum("price * quantity")

***ANSWER NOT DONE YET!!!***

9.  Simulate buying an item by inserting a User for yourself and an Order for that User.
    User.create(first_name: "Mike", last_name: "Hughes", email: "hughes@mike.com")
    Order.create(user_id: (Order.count + 1), item_id:



## Hard Mode

1. What item was ordered most often? Grossed the most money?
Query -  
Answer - 

2. What user spent the most?
Query -  
Answer - 

3. What were the top 3 highest grossing categories?
Query -  
Answer - 


























