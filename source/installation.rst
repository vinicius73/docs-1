Installation 
==============

To install Alter you need to clone the repository and pull all the alter git submodules, enter in your theme folder and run:

.. code-block:: shell

	git clone git@github.com:alterfw/alter.git alter
	cd alter;
	git pull && git submodule init && git submodule update && git submodule status
	git submodule foreach --recursive git submodule update --init

After this, add this line to your **functions.php**:

.. code-block:: php
	
	<?php

	require_once "alter/core/main.php";