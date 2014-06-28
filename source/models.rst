Models
===============

Models in Alter are named by convetion over configuration. Before creating a model, you need to create a folder named `model` in your theme folder root, all model files must me created into this directory.

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