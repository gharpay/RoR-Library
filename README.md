RoR-Library
===========

GharPay - a gem for managing Cash on Delivery for GharPay service

##Installation

Add the following line to your Gemfile

###Rails (4)


```
gem 'gharpay', :git => 'https://github.com/joshsoftware/gharpay.git'
```

###Rails (3.x)

```
gem 'gharpay', :git => 'https://github.com/joshsoftware/gharpay.git'
```

##Sample Usage

Create an initilizer to store your Gharpay API Key & Secret

`config/initializers/gharpay.rb`

```ruby
  ENV["gharpay_key"] = "foo" 
  ENV["gharpay_secret"] = "bar"
```
_* You must restart your Rails server if it is already running, in order for this step to work._

####Create an order

```ruby
gharpay = Gharpay::Base.new ENV["gharpay_key"], ENV["gharpay_secret"]
customer_details = {"firstName" => "Foo", "lastName" => "Bar", "contactNo" => "9999999999", "address" => "Foo"
order_details = {"deliveryDate" => Date.today.strftime("%d-%m-%Y"), "orderAmount" => "2000", "clientOrderID" => "1234", "pincode" => "123456"}
data = {"customerDetails" => customer_details, "orderDetails" => :order_details}
gharpay_order_id = gharpay.create_order data
```

####View Order Status
Returns the status of the order, as per the Gharpay documentation - eg. `Delivered`, `Pending`, etc.
```ruby
gharpay = Gharpay::Base.new ENV["gharpay_key"], ENV["gharpay_secret"]
gharpay.view_order_status gharpay_order_id #where gharpay_order_id is a Gharpay Order ID eg. GW-123-345
```

