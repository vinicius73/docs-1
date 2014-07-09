Models
===============

Models in Alter are named by convetion over configuration. Before creating a model, you need to create a folder named **model** in your theme folder root, all model files must me created into this directory.

Models are directly linked to Wordpress Post Types. So, if you create a model called `BookModel`, Alter will register the `Book` Post Type.


Creating Models
^^^^^^^^^^^^^^^

To create a model is very simple, you need to use this convention to name the class: `<Entity name>Model`; 

See the example:

.. code-block:: php
	
	<?php

	class CarModel extends AppModel{

	}


Setting Model fields	
^^^^^^^^^^^^^^^^^^^^

To set fields in your model just create a instance variable called `fields` with the fields that you want in that post type.

.. code-block:: php

	<?php

	class CarModel extends AppModel{

	    public $fields = array(
	        'editor' => true,
	        'title' => true,
	        'thumbmail' => true     
	    );

	}


Custom fields	
^^^^^^^^^^^^^

Alter uses the `rw-meta-box <https://github.com/rilwis/meta-box>`_ to create custom fields in your post type. To set your custom fields in the model you need to specify the label and the type of the field:

.. code-block:: php

	<?php

	class CarModel extends AppModel{

	    public $fields = array(

	        // Default Wordpress Fields
	        'editor' => true,
	        'title' => true,
	        'thumbmail' => true ,

	        // Custom Fields
	        'manufacturer' => array(
	            'label' => 'Manufacturer',
	            'type' => 'text'
	        )

	    );

	}

The types available are:

- text
- long_text
- int
- float
- boolean
- image
- file	
  
All fields and settings available in https://github.com/rilwis/meta-box#supported-fields


Multiple custom fields
^^^^^^^^^^^^^^^^^^^^^^

To set that the custom field may has more than one item you can set the **multiple** parameter to true:


.. code-block:: php

	<?php

	class CarModel extends AppModel{

	    public $fields = array(

	        // Default Wordpress Fields
	        'editor' => true,
	        'title' => true,
	        'thumbmail' => true ,

	        // Custom Fields
	        'manufacturer' => array(
	            'label' => 'Manufacturer',
	            'type' => 'text'
	        ),

	        'photo' => array(
	            'label' => 'Photo Gallery',
	            'type' => 'image',
	            'multiple' => true
	        )

	    );

	}

Setting up a route
^^^^^^^^^^^^^^^^^^

Route is the path that your posts of a model will be accessible to the public. In the example above, my posts of type **book** will be accessible in http://mysite.com/books:

.. code-block:: php

	<?php

	class CarModel extends AppModel{

		public $route = 'books';


Labels and icon for the Wordpress Admin
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You can setup the labels with two attributes of a model object: singular and plural. You can also specify a icon for the Post Type in the Wordpress Admin

.. code-block:: php

	<?php

	class CarModel extends AppModel{

		public $singular = "Car";
  		public $plural = "Cars";
    
  		public $icon = "dashicons-admin-home";

Overriding options.
^^^^^^^^^^^^^^^^^^^

You can manipulate any extra option register_post_type_ you want.

.. code-block:: php

	<?php

	class CarModel extends AppModel{

		public $args = array(
			'public' => false
		);

		public $labels = array(
			'not_found' => 'Nothing to show here.'
		);

There are more options available that you can override.

.. code-block:: php

	<?php

	class CarModel extends AppModel{

		public $fields = array();
		public $taxonomies = array();
		public $labels = array();
		public $capabilities = array();
		public $args = array();
		public $supports = array();
		public $icon = 'dashicons-admin-post';
		public $capability_type = 'page';
		public $text_domain = 'text_domain';
		public $singular;
		public $plural;
		public $description;
		public $route;


Linking a model to a taxonomy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You can easily link a model to one or more taxonomies, see:

.. code-block:: php

	<?php

	class CarModel extends AppModel{

		public $taxonomies = array('car_type', 'car_color'); 		
	

Retrieve items from Model	
^^^^^^^^^^^^^^^^^^^^^^^^^

The model has some methods to retrieve information. You can you use `find($limit = null)`, `findById($id)`, `findBySlug($slug)` or `findByTaxonomy($taxonomy, $term, $limit)`, these methods returns an array or a item of **PostObject**. 

See the example:

.. code-block:: php

	<?php

	$cars = $app->car->find();

The `find()` method can receive an array of parameters, for example:

.. code-block:: php

	<?php	

	$cars = $app->car->find(array('limit'=>5));

And if you need to pass a Wordpress query ou can do also:	

.. code-block:: php

	<?php	

	$cars = $app->car->find(array(
    	'query' => 'posts_per_page=5'
	));


Model find() automatic methods	
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^	

If you want to find posts from a custom field, you can call `findBy<Attribute>()`, for example:

.. code-block:: php

	<?php	

	$cars = $app->car->findByManufacturer("Wolks");

You can use the find automagic method for all custom fields and also for ID, author, date, category and status.	


Paginate	
^^^^^^^^

With the model you can also paginate the results using the paginate method. For example, if you need 5 items per page:

.. code-block:: php

	<?php	

	$cars = $app->car->paginate(5);

But if you want to use the `posts_per_page` wordpress option can just call `paginate` without any parameter.	


The PostObject
^^^^^^^^^^^^^^

The PostObejct is an object that contains **all the properties** of an Wordpress entry and his custom fields, let's see an example using your Car model:

.. code-block:: php

	public 'ID' => int 45
	public 'author' => string '1' (length=1)
	public 'date' => string '2014-05-04 13:42:59' (length=19)
	public 'date_gmt' => string '2014-05-04 13:42:59' (length=19)
	public 'content' => string 'An example car' (length=14)
	public 'title' => string 'Fusca' (length=5)
	public 'excerpt' => string '' (length=0)
	public 'status' => string 'publish' (length=7)
	public 'comment_status' => string 'closed' (length=6)
	public 'ping_status' => string 'closed' (length=6)
	public 'password' => string '' (length=0)
	public 'name' => string 'fusca' (length=5)
	public 'to_ping' => string '' (length=0)
	public 'pinged' => string '' (length=0)
	public 'modified' => string '2014-05-04 13:42:59' (length=19)
	public 'modified_gmt' => string '2014-05-04 13:42:59' (length=19)
	public 'content_filtered' => string '' (length=0)
	public 'parent' => int 0
	public 'guid' => string 'http://wp/wordpress/?post_type=car&#038;p=45' (length=44)
	public 'menu_order' => int 0
	public 'type' => string 'car' (length=3)
	public 'mime_type' => string '' (length=0)
	public 'comment_count' => string '0' (length=1)
	public 'filter' => string 'raw' (length=3)
	public 'manufacturer' => string 'Wolks' (length=5)
	public 'photo' => 
	  array (size=3)
	    0 => 
	      object(stdClass)[103]
	        public 'thumbnail' => string 'http://wp/wordpress/wp-content/uploads/2014/05/13991386118211-150x150.png' (length=73)
	        public 'medium' => string 'http://wp/wordpress/wp-content/uploads/2014/05/13991386118211-300x225.png' (length=73)
	        public 'large' => string 'http://wp/wordpress/wp-content/uploads/2014/05/13991386118211.png' (length=65)
	    1 => 
	      object(stdClass)[95]
	        public 'thumbnail' => string 'http://wp/wordpress/wp-content/uploads/2014/05/13991386201661-150x150.png' (length=73)
	        public 'medium' => string 'http://wp/wordpress/wp-content/uploads/2014/05/13991386201661-300x225.png' (length=73)
	        public 'large' => string 'http://wp/wordpress/wp-content/uploads/2014/05/13991386201661.png' (length=65)
	    2 => 
	      object(stdClass)[105]
	        public 'thumbnail' => string 'http://wp/wordpress/wp-content/uploads/2014/05/1399205647180-150x150.png' (length=72)
	        public 'medium' => string 'http://wp/wordpress/wp-content/uploads/2014/05/1399205647180-300x225.png' (length=72)
	        public 'large' => string 'http://wp/wordpress/wp-content/uploads/2014/05/1399205647180.png' (length=64)

As you can see the custom fields `manufacturer` and `photo` can be accessed by simple doing `$post->manufacturer`.	        

.. _register_post_type: http://codex.wordpress.org/Function_Reference/register_post_type#Arguments