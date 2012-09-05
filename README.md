## Lara Cart
**Version: 1.0**

A Shopping Cart Bundle for Laravel, based on the Cart library from CodeIgniter.

## Installation
Clone the project into **bundles/lara-cart**

Then, update your bundles.php to auto-start the bundle.

    return array(
        'lara-cart' => array( 'auto' => true )
    );

Then move the **public** folder outside the **bundles/lara-cart** folder.
    
## Viewing the Example
Just navigate to the page **cart**, example

    http://laravel.local/public/cart
    
## Adding an Item to The Cart
To add an item to the shopping cart, simply pass an array with the product information to the Cart::add() method, as shown below:

    $item = array(
        'id'      => 'sku_123ABC',
        'qty'     => 1,
        'price'   => 39.95,
        'name'    => 'T-Shirt',
        'options' => array(
            'Size'  => 'L', 
            'Color' => 'Red'
        )
    );
    
    Cart::add( $item );


####Important:
    The first four array indexes above (id, qty, price, and name) are required.
    If you omit any of them the data will not be saved to the cart.
    The fifth index (options) is optional.
    It is intended to be used in cases where your product has options associated with it.
    Use an array for options, as shown above.
    
**The five reserved indexes are:**
- **id** - Each product in your store must have a unique identifier. Typically this will be an "sku" or other such identifier.
- **qty** - The quantity being purchased.
- **price** - The price of the item.
- **name** - The name of the item.
- **options** - Any additional attributes that are needed to identify the product. These must be passed via an array.

In addition to the five indexes above, there are two reserved words: **rowid** and **subtotal**. These are used internally by the Cart class, so please do NOT use those words as index names when inserting data into the cart.

Your array may contain additional data. Anything you include in your array will be stored in the session. However, it is best to standardize your data among all your products in order to make displaying the information in a table easier.

The add() method will return the $rowid if you successfully insert a single item.

## Adding Multiple Items to The Cart
By using a multi-dimensional array, as shown below, it is possible to add multiple products to the cart in one action. This is useful in cases where you wish to allow people to select from among several items on the same page.

    $items = array(
        array(
            'id'      => 'sku_123ABC',
            'qty'     => 1,
            'price'   => 39.95,
            'name'    => 'T-Shirt',
            'options' => array(
                'Size'  => 'L', 
                'Color' => 'Red'
            )
        ),
        array(
            'id'      => 'sku_567ZYX',
            'qty'     => 1,
            'price'   => 9.95,
            'name'    => 'Coffee Mug'
        ),
        array(
            'id'      => 'sku_965QRS',
            'qty'     => 1,
            'price'   => 29.95,
            'name'    => 'Shot Glass'
        )
    );

    Cart::add( $items );

 
## Updating the Cart
To update the information in your cart, you must pass an array containing the Row ID and quantity to the Cart::update() method:

####Note:
    If the quantity is set to zero, the item will be removed from the cart.

**Updating a single item:**

    $item = array(
        'rowid' => 'b99ccdf16028f015540f341130b6d8ec',
        'qty'   => 3
    );

    Cart::update( $item ); 


**Updating multiple items:**

    $items = array(
        array(
            'rowid' => 'b99ccdf16028f015540f341130b6d8ec',
            'qty'   => 3
        ),
        array(
            'rowid' => 'xw82g9q3r495893iajdh473990rikw23',
            'qty'   => 4
        ),
        array(
            'rowid' => 'fh4kdkkkaoe30njgoe92rkdkkobec333',
            'qty'   => 2
        )
    );

    Cart::update( $items );


####What is a Row ID?
The row ID is a unique identifier that is generated by the cart code when an item is added to the cart. The reason a unique ID is created is so that identical products with different options can be managed by the cart.

For example, let's say someone buys two identical t-shirts (same product ID), but in different sizes. The product ID (and other attributes) will be identical for both sizes because it's the same shirt. The only difference will be the size. The cart must therefore have a means of identifying this difference so that the two sizes of shirts can be managed independently. It does so by creating a unique "row ID" based on the product ID and any options associated with it.

In nearly all cases, updating the cart will be something the user does via the "view cart" page, so as a developer, it is unlikely that you will ever have to concern yourself with the "row ID", other then making sure your "view cart" page contains this information in a hidden form field, and making sure it gets passed to the update function when the update form is submitted. Please examine the construction of the "view cart" page above for more information.
    
    
    
## Removing items from the Cart
To remove an item from your cart, you must pass the Row ID to the Cart::remove() method:

    Cart::remove('fh4kdkkkaoe30njgoe92rkdkkobec333');


## Displaying the Cart
To display the cart you will create a view file with code similar to the one shown below.

TODO..


## Function Reference

    Cart::add();
Permits you to add items to the shopping cart.

    Cart::update();
Permits you to update items in the shopping cart.

    Cart::remove(rowid);
Permits you to remove an item from the shopping cart.

    Cart::total();
Displays the total amount in the cart.

    Cart::total_items();
Displays the total number of items in the cart.

    Cart::contents();
Returns an array containing everything in the cart.

    Cart:has_options(rowid);
Returns TRUE (boolean) if a particular row in the cart contains options. This function is designed to be used in a loop with Cart::contents(), since you must pass the rowid to this function, as shown in the Displaying the Cart example above.

    Cart::product_options(rowid);
Returns an array of options for a particular product. This function is designed to be used in a loop with Cart::contents(), since you must pass the rowid to this function, as shown in the Displaying the Cart example above.

    Cart::destroy();
Permits you to destroy the cart. This function will likely be called when you are finished processing the customer's order.


## Credits
    CodeIgniter for writing this Library.
    Twitter for the awesome Bootstrap framework.

    
    