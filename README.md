This folder structure should be suitable for starting a project that uses a database:

* Fork this repo
* Clone this repo
* Run `bundle install` to install `active_record`
* `rake generate:migration <NAME>` to create a migration (Don't include the `<` `>` in your name, it should also start with a capital)
* `rake db:migrate` to run the migration and update the database
* Create models in lib that subclass `ActiveRecord::Base`
* ... ?
* Profit

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

9.  Simulate buying an item by inserting a User for yourself and an Order for that User.
    User.create(first_name: "Mike", last_name: "Hughes", email: "hughes@mike.com")
    Order.create(user_id: (Order.count + 1), item_id:

## Rundown

```
.
├── Gemfile             # Details which gems are required by the project
├── README.md           # This file
├── Rakefile            # Defines `rake generate:migration` and `db:migrate`
├── config
│   └── database.yml    # Defines the database config (e.g. name of file)
├── console.rb          # `ruby console.rb` starts `pry` with models loaded
├── db
│   ├── dev.sqlite3     # Default location of the database file
│   ├── migrate         # Folder containing generated migrations
│   └── setup.rb        # `require`ing this file sets up the db connection
└── lib                 # Your ruby code (models, etc.) should go here
    └── all.rb          # Require this file to auto-require _all_ `.rb` files in `lib`
```














