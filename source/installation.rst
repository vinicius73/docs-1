Installation 
==============

To install Alter you need to clone the repository and pull all the alter git submodules, enter in your theme folder and run:

.. code-block:: shell

	git clone git@github.com:alterfw/alter.git alter

Then install Alter dependencies:	

.. code-block:: shell
	
	cd alter; composer install	


After this, add this line to your **functions.php**:

.. code-block:: php
	
	<?php

	require_once "alter/core/main.php";