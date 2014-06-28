Application Configuration
=========================

Using the **App** class you can set set some configuration about your theme aplication.

Ensures that a page will exists on theme activation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In some cases your theme can be based on essential pages that must exist to your theme work perfectly. In this cases you can create a page via configuration, if they not exists:

.. code-block:: php
	
	<?php

	$app->defaultPage('My page', 'my-page');

This method returns an ID of the created page, the signature is:

.. code-block:: php

	defaultPage($page, $slug, $parent_id, $content);	


Setup Wordpress to use SMTP server
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In some cases your host doesn't supports the PHP `mail()` function and you need to setup a SMTP server. But, you don't need a plugin to do this, right?

You can setup your SMTP following this example:

.. code-block:: php
	
	<?php

	$app->SMTP('myhost.com', 'user@myhost.com', 'myPassword', 587);

The method signature is:

.. code-block:: php	

	SMTP($host, $user, $password, $port = 587, $ssl = false);

Creating Taxonomies
^^^^^^^^^^^^^^^^^^^

It's very simple to register taxonomies with Alter, see:	

.. code-block:: php
	
	<?php

	$app->registerTaxonomy('city', 'City', 'Cities');
	$app->registerTaxonomy('province', 'Province', 'Provinces');
	$app->registerTaxonomies();
