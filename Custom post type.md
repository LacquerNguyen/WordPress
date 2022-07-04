# Custom post type
function create_department()
{
    /*
     * Biến $label để chứa các text liên quan đến tên hiển thị của Post Type trong Admin
     */
    $label = array(
        'name' => 'Department', 
        'singular_name' => 'Department'
    );

    /*
     * Biến $args là những tham số quan trọng trong Post Type
     */
    $args = array(
        'labels' => $label, 
        'description' => 'Department', 
        'supports' => array(
            'title',
            'editor',
            'excerpt',
            'author',
            'thumbnail',
            'comments',
            'trackbacks',
            'revisions',
            'custom-fields'
        ),
        'taxonomies' => array( 'department-category', 'post_tag' ), 
        'hierarchical' => false, 
        'public' => true,
        'show_ui' => true, 
        'show_in_menu' => true, 
        'show_in_nav_menus' => true, 
        'show_in_admin_bar' => true, 
        'menu_position' => 5, 
        'menu_icon' => ”, 
        'can_export' => true,
        'has_archive' => true,
        'exclude_from_search' => false, 
        'publicly_queryable' => true, 
        'capability_type' => 'post' 
    );


    register_post_type('department', $args);

}
/* Kích hoạt hàm tạo custom post type */
add_action('init', 'create_department');

/**
 * Add custom taxonomies
 *
 * Additional custom taxonomies can be defined here
 * https://codex.wordpress.org/Function_Reference/register_taxonomy
 */
function add_custom_taxonomies() {
  // Add new "Locations" taxonomy to Posts
  register_taxonomy('department-category', 'post', array(
    // Hierarchical taxonomy (like categories)
    'hierarchical' => true,
    // This array of options controls the labels displayed in the WordPress Admin UI
    'labels' => array(
      'name' => _x( 'Department Category', 'taxonomy general name' ),
      'singular_name' => _x( 'Department Category', 'taxonomy singular name' ),
      'search_items' =>  __( 'Search Department Category' ),
      'all_items' => __( 'All Department Category' ),
      'parent_item' => __( 'Parent Department Category' ),
      'parent_item_colon' => __( 'Parent Department Category:' ),
      'edit_item' => __( 'Edit' ),
      'update_item' => __( 'Update' ),
      'add_new_item' => __( 'Add New' ),
      'new_item_name' => __( 'New Department Category Name' ),
      'menu_name' => __( 'Department Category' ),
    ),
    // Control the slugs used for this taxonomy
    'rewrite' => array(
      'slug' => 'departments', // This controls the base slug that will display before each term
      'with_front' => false, // Don't display the category base before "/locations/"
      'hierarchical' => true // This will allow URL's like "/locations/boston/cambridge/"
    ),
  ));
}
add_action( 'init', 'add_custom_taxonomies', 0 );

function my_change_posts_order( $query ){
    if (is_tax( 'department-category', $taxonomy_term_object )) {
        $query->set( 'order', 'ASC' );
    }
};
add_action( 'pre_get_posts', 'my_change_posts_order'); 
