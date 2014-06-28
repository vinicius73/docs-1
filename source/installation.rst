Installation 
==============

To install Alter you need to clone the repository and pull all the alter git submodules, enter in your theme folder and run:

.. code-block:: shell

	git clone git@github.com:sergiovilar/alter.git alter
	cd alter;
	git pull && git submodule init && git submodule update && git submodule status
	git submodule foreach --recursive git submodule update --init