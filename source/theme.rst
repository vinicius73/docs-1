Theme
===============

Alter has a class that helps you with several common in developing themes for WordPress tasks so that it has the global variable $appTheme

You just need to call there in your functions.php

.. code-block:: php
	
	<?php

	require_once 'vendor/autoload.php';

	global $appTheme;

It is very simple to work with.

.. code-block:: php
	
	<?php

	global $appTheme;
	// $appTheme->addMenu($location, $description);
	// $appTheme->addThemeSupport($feature);
	// $appTheme->addImageSize($name, $width, $height, $crop);
	// $appTheme->addPostTypeSupport($post_type, $feature);
	$appTheme->addMenu('main_menu', 'Main Menu');
	$appTheme->addImageSize('page-thumbnail, 960, 400);
	$appTheme->addPostTypeSupport('page', 'excerpt');


In most cases the syntax of the function is equal to the equivalent in WordPress. The benefit here is that the Alter stack their commands and only run on WordPress when they really are needed.

Theme Assets	
^^^^^^^^^^^^

One of the best features you have at your disposal is the organization called assets (css and javascrpt) their themes.

.. code-block:: php
	
	<?php

	global $appTheme;
	// Css
	// $appTheme->addCss($handle, $src, $deps, $ver, $media);
	$appTheme->addCss('main', 'assets/css/main.min.css');
	$appTheme->addCss('g-font', 'http://fonts.googleapis.com/css?family=Open+Sans');

	// Js
	// $appTheme->addJs($handle, $src, $deps, $ver, $in_footer);
	// $appTheme->addJsToFooter($handle, $src, $deps, $ver);
	// $appTheme->addJsToHead($handle, $src, $deps, $ver);
	$appTheme->addJsToHead('modernizr', 'assets/js/vendor/modernizr-2.6.2-respond-1.1.0.min.js', null, '2.6.2');
	$appTheme->addJsToFooter('app', 'assets/js/app.min.js');

	// Support the jQuery CDN :)
	// $appTheme->setJqueryCDNSupport($version, $fallback);
	$appTheme->setJqueryCDNSupport('2.1.1', 'assets/js/vendor/jquery-2.1.1.min.js');

View files by registered Alter is very easy, just call **wp_head ()** and **wp_footer ()** on their places properly.

.. code-block:: php
	
	<html>
		<head>
			...
			<?php wp_head(); ?>
		</head>
		<body>
			...
			<?php wp_footer(); ?>
		</body>
	</html>