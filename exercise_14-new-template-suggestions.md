#### Drupal 8 Theming

# Exercise 14: 

## Create new template suggestions

In drupal 7, we used to create new template suggestions in our preprocess functions. In drupal 8, we use two new functions to create new suggestions for a twig templates.

These functions are `hook_theme_suggestions_alter()` function and the more targeted, `hook_theme_suggestions_HOOK_alter()` function. The `HOOK` refers to the theme hook being used, like 'node' or 'page' or 'menu_link'. This `HOOK` helps to focus in your suggestions to a specific theme component. In this exercise we will create new suggestions for our 'node' templates based off if the user is logged in or not.

1. Open the **acme.theme** file and add the following function:

	```
	function acme_theme_suggestions_node_alter(&$suggestions, $variables, $hook) {
		// Our code will go here.
	}	
	```

2. Inside of our new function, add the following code:

	```
	...
	
	if (\Drupal::currentUser()->isAuthenticated()) {
		$bundle = $variables['elements']['#node']->bundle();
		$mode = $variables['elements']['#view_mode'];
		$view_mode = strtr($mode, '.', '_');
	
		$suggestions[] = 'node__' . $bundle . '__logged_in';
  		$suggestions[] = 'node__' . $view_mode . '__logged_in';
	}
	
	...
	```
	This will create a new suggestion for Content types and Node view modes for when the viewer is logged in.

3. Clear you caches and visit a node page. View the source code and see if you an find your new template suggestions at the start of your node output. 


## Questions you may have...
+ What is a theme suggestion HOOK?


## Done ☺