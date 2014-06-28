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