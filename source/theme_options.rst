Theme Options
===================

Developing themes for wordpress is not always easy, are not rare veses when faced with an annoying situation to resolve. 
For this there is the Theme Options, to facilitate and provide flexibility to our work. 

Alter an interface to the quite satisfactory development of theme settings. Its use is easy and it has enough options. 
Alter works in conjunction with option-tree_ development theme options.

Simply create a file in the root of your theme called **ThemeOptions.php ** and create a class called ThemeOptions that extends **OptionTree**

.. code-block:: php
	
	<?php

		class ThemeOptions extends OptionTree
		{
			protected $page_title = 'My Theme Options';
			protected $menu_title = 'Menu Theme Options';
			protected $settings_id = 'my_theme_name';

			// optional 
			protected $header_logo = null;
			protected $header_version_text = null;
			protected $header_logo_link = null;
			protected $show_new_layout = false;
			protected $show_docs = false;
			protected $show_pages = false;

			protected $contextual_help
				= array(
					'content' => array(
						array(
							'id'=> 'info_one',
							'title'   => 'Theme data',
							'content' => 'You can put whatever you want here.'
						)
					),
					'sidebar' => ''
				);

			// His command of sections and fields.
			public function doRegister()
			{
				// Begins a section.
				$this->addSection('opt_general', 'Geral')
					// Section fields.
					->addUpload('general_logo', 'Logo', 'Site's logo [280x85]');
					->addText('general_logo_title', 'Title logo.', 'Enter the text that will be the description of the logo.');

				// Begins a section.
				$this->addSection('opt_anyone', 'Anyone')
					// Section fields.
					->addTextarea('opt_id', 'OPT Title.', 'OPT Desc.' ,'default value' ,null , array('rows'=>'15'));
			}
		}			

The theme options are separated into sections, which facilitates the organization who develops and understanding who uses.

Fields available.
^^^^^^^^^^^^^^^^^

- -> **addText** ($id, $label, $desc = null, $std = null, $section = null, array $extra = array()) // *text*
- -> **addTextarea** ($id, $label, $desc = null, $std = null, $section = null, array $extra = array()) // *textarea*
- -> **addSelect** ($id, $label, array $choices, $desc = null, $std = null, $section = null, array $extra = array()) // *field of type select.*
- -> **addCheckbox** ($id, $label, array $choices, $desc = null, $std = null, $section = null, array $extra = array()) // *field of type checkbox.*
- -> **addRadio** ($id, $label, array $choices, $desc = null, $std = null, $section = null, array $extra = array()) // *field of type radio.*
- -> **addWYSIWYG** ($id, $label, $desc = null, $std = null, $section = null, array $extra = array()) // *WYSIWYG*
- -> **addUpload** ($id, $label, $desc = null, $std = null, $section = null, array $extra = array()) // *upload (image)*
- -> **addCustomPostTypeSelect** ($id, $label, $desc = null, $postType = 'post', $std = null, $section = null, array $extra = array()) // *select type field with custom post type*
- -> **addCustomPostTypeCheckbox** ($id, $label, $desc = null, $postType = 'post', $std = null, $section = null, array $extra = array()) // *checkbox type field with custom post type*
- -> **addPageSelect** ($id, $label, $desc = null, $std = null, $section = null, array $extra = array()) // *select type field with post type page*
- -> **addPageCheckbox** ($id, $label, $desc = null, $std = null, $section = null, array $extra = array()) // *checkbox type field with post type page*
- -> **addPostCheckbox** ($id, $label, $desc = null, $std = null, $section = null, array $extra = array()) // *checkbox type field with post type post*
- -> **addPostSelect** ($id, $label, $desc = null, $std = null, $section = null, array $extra = array()) // *select type field with post type post*
- -> **addTaxonomySelect** ($id, $label, $desc = null, $taxonomy = 'category', $std = null, $section = null, array $extra = array()) // *select type field with taxonomy*
- -> **addTaxonomyCheckbox** ($id, $label, $desc = null, $taxonomy = 'category', $std = null, $section = null, array $extra = array()) // *checkbox type field with taxonomy*
- -> **addCategorySelect** ($id, $label, $desc = null, $std = null, $section = null, array $extra = array()) // *select type field with categories*
- -> **addCategoryCheckbox** ($id, $label, $desc = null, $std = null, $section = null, array $extra = array()) // *checkbox type field with categories*
- -> **addTagSelect** ($id, $label, $desc = null, $std = null, $section = null, array $extra = array()) // *select type field with tags*
- -> **addTagCheckbox** ($id, $label, $desc = null, $std = null, $section = null, array $extra = array()) // *checkbox type field with tags*
- -> **addTypography** ($id, $label, $desc = null, $std = null, $section = null, array $extra = array())
- -> **addOnOff** ($id, $label, $desc = null, $std = null, $section = null, array $extra = array())
- -> **addOption** (array $args) // Raw data for option.
  
All **$section** arguments are optional, if it is not spent is automatically registered adiconado last section.



.. _option-tree: https://github.com/valendesigns/option-tree