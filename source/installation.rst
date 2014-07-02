Installation 
==============

Create a `composer.json` for your theme:

.. code-block:: shell

	composer init

Then add to your `composer.json`:

.. code-block:: json
	
	"minimum-stability": "dev",
	"require": {
		"alterfw/alter": "dev-master"
	}

Run composer:

.. code-block:: json

	composer install

After this, add this line to your **functions.php**:

.. code-block:: php

	require_once "vendor/autoload.php";
