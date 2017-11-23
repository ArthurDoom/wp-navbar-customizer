# wp-navbar-customizer
Adding an option to the wordpress customizer to switch between navbar styles.

## Initiate the customizer
Add this to your themes functions.php

```php
function mytheme_customize_register( $wp_customize ) {
   //All our sections, settings, and controls will be added here
	 $wp_customize->add_section( 'my_theme_style_section' , array(
			 'title'      => __( 'Style', 'my_theme' ), //The title of the section
			 'priority'   => 30, //Where we are in the order of options
	 ) );

		$wp_customize->add_control( 'my_theme_nav', array(
        'label'    => 'Navigation Background', //The title
        'section'  => 'my_theme_style_section', //What section the options are in
        'settings' => 'my_theme_nav_settings', //Our settings
        'type'     => 'radio', //The type
        'choices'  => array(
            'dark' => 'Dark',
            'light'  => 'Light',
            ),
        )
    );
}
add_action( 'customize_register', 'mytheme_customize_register' );
```

## Add class function
This adds a class with an option to mannualy add classes in our themes code. Using bootstrap as an example.

```php
function nav_class( $class = '' ) {
	$navStyle = get_theme_mod( 'ew_nav_settings' );
	if ( $navStyle  == 'dark' ) {
			echo 'class="' . $class . ' navbar-inverse"';
  }
	if ( $navStyle  == 'light' ) {
			echo 'class="' . $class . ' navbar-default"';
  }
}
```

## Implementation 
An example with added class navbar with navbar-inverse or navbar-default used depending on what option selected.

```php
<nav <?php nav_class("navbar"); ?>>...</nav>
```
