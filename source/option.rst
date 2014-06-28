Options Pages
============

You can use options page to provide additional configuration and customization to your website, to create a options page is very similar to creating models.

As models, options page follows the configuration over convention but in this case has no convention to name the class. Before creating a options page, you need to create a folder named **option** in your theme folder root, all options page files must me created into this directory.

Creating an Options Page
^^^^^^^^^^^^^^^^^^^^^^^^

As we said, it's very similar to models:

.. code-block:: php

	<?php

	class MyPage extends OptionPage{

	    public $title = 'My Options page';
	    public $capability = 'switch_themes';

	    public $fields = array(

	        'address' => array(
	            'label' => 'Address',
	            'type' => 'text'
	        ),

	        'email' => array(
	            'label' => 'Email',
	            'type' => 'text'
	        )
	    )

	}



