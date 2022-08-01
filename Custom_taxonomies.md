# WordPress
```php
function career_custom_taxonomies() {
  // Add new "Locations" taxonomy to Posts
  register_taxonomy('career-category', 'career', array(
    // Hierarchical taxonomy (like categories)
    'hierarchical' => true,
    // This array of options controls the labels displayed in the WordPress Admin UI
    'labels' => array(
      'name' => _x( 'Career Category', 'taxonomy general name' ),
      'singular_name' => _x( 'Career Category', 'taxonomy singular name' ),
      'search_items' =>  __( 'Search Career Category' ),
      'all_items' => __( 'All Career Category' ),
      'parent_item' => __( 'Parent Career Category' ),
      'parent_item_colon' => __( 'Parent Career Category:' ),
      'edit_item' => __( 'Edit' ),
      'update_item' => __( 'Update' ),
      'add_new_item' => __( 'Add New' ),
      'new_item_name' => __( 'New Career Category Name' ),
      'menu_name' => __( 'Career Category' ),
    ),
    // Control the slugs used for this taxonomy
    'rewrite' => array(
      'slug' => 'careers', // This controls the base slug that will display before each term
      'with_front' => false, // Don't display the category base before "/locations/"
      'hierarchical' => true // This will allow URL's like "/locations/boston/cambridge/"
    ),
  ));
}
add_action( 'init', 'career_custom_taxonomies', 0 );


function my_change_posts_order( $query ){
    if (is_tax( 'department-category', $taxonomy_term_object )) {
        $query->set( 'order', 'ASC' );
    }
};


```
