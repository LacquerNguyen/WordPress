# WordPress
```html
<?php
function gdit_themes_setup() {
//add_theme_support( 'title-tag' );
add_theme_support( 'post-thumbnails' );
add_image_size( 'news-thumb', 513, 322, true );
add_image_size( 'development-thumb', 488, 411, true );
add_image_size( 'development-detail', 265, 500, true );
add_image_size( 'interview-img', 242, 363, true );
register_nav_menus( array(
	'top'    => __( 'Top Menu', 'gdit' ),
	'footer'    => __( 'Footer Menu', 'gdit' ),
	'sitemap'    => __( 'Sitemap', 'gdit' ),
));
// Add theme support for selective refresh for widgets.
add_theme_support( 'customize-selective-refresh-widgets' );
}
add_action( 'after_setup_theme', 'gdit_themes_setup' );

register_sidebar( array(
	'name'          => __( 'Sidebar', 'gdit' ),
	'id'            => 'sidebar-1',
	'description'   => __( 'Add widgets here to appear in your sidebar on blog posts and archive pages.', 'gdit' ),
	'before_widget' => '<section id="%1$s" class="widget %2$s">',
	'after_widget'  => '</section>',
	'before_title'  => '<h2 class="widget-title">',
	'after_title'   => '</h2>',
) );

register_sidebar( array(
	'name'          => __( 'Career Recruit', 'gdit' ),
	'id'            => 'career-recruit',
	'description'   => __( 'Add widgets here to appear in your sidebar on blog posts and archive pages.', 'gdit' ),
	'before_widget' => '<section id="%1$s" class="widget %2$s">',
	'after_widget'  => '</section>',
	'before_title'  => '<h2 class="widget-title">',
	'after_title'   => '</h2>',
) );

register_sidebar( array(
	'name'          => __( 'Intern Recruit', 'gdit' ),
	'id'            => 'intern-recruit',
	'description'   => __( 'Add widgets here to appear in your sidebar on blog posts and archive pages.', 'gdit' ),
	'before_widget' => '<section id="%1$s" class="widget %2$s">',
	'after_widget'  => '</section>',
	'before_title'  => '<h2 class="widget-title">',
	'after_title'   => '</h2>',
) );


add_filter('wp_trim_excerpt', function($text){    
   $max_length = 500;

   if(mb_strwidth ($text) > $max_length){
     $text = mb_substr($text, 0, $max_length, 'UTF-8');
   }

   return $text;
});

function the_field_multilang($content){
	echo get_field_multilang($content);
}
function get_field_multilang($content){
	$result = '';
	switch (ICL_LANGUAGE_CODE) {
		case 'vi':
			$result = get_field($content,11);
			break;
		case 'en':
			$result = get_field($content,9);
			break;
		
		default:
			$result = get_field($content,2);
			break;
	}
	return $result;
}
function echo_lang($jp,$vi,$en){
	echo get_lang($jp,$vi,$en);
}
function get_lang($jp,$vi,$en){
	switch (ICL_LANGUAGE_CODE) {
		case 'vi':
			return $vi;
			break;
		case 'en':
			return $en;
			break;
		
		default:
			return $jp;
			break;
	}
}
function get_string_lang($str_name){
	switch ($str_name) {
		case 'no_js':
			return get_lang(
				'このサイトではJavaScriptを使用したコンテンツ・機能を提供しています。JavaScriptを有効にするとご利用いただけます。',
				'このサイトではJavaScriptを使用したコンテンツ・機能を提供しています。JavaScriptを有効にするとご利用いただけます。',
				'このサイトではJavaScriptを使用したコンテンツ・機能を提供しています。JavaScriptを有効にするとご利用いただけます。');
			break;
		case 'honbun':
			return get_lang(
				'本文へスキップします。',
				'本文へスキップします。',
				'本文へスキップします。');
			break;
		case 'honbun_target':
			return get_lang(
				'ここから本文です。',
				'ここから本文です。',
				'ここから本文です。');
			break;
		case 'back_to_top':
			return get_lang(
				'ページの先頭へ戻る',
				'Trở về đầu trang',
				'Back to top');
			break;
		case 'search':
			return get_lang(
				'検索',
				'Tìm kiếm',
				'Search');
			break;
		case 'close':
			return get_lang(
				'閉じる',
				'Đóng',
				'Close');
			break;
		case 'read_more': 
			return get_lang(
				'続きを読む',
				'Xem thêm',
				'Read more');
		default:
			return '';
			break;
	}
}
function show_string_lang($str_name){
	echo get_string_lang($str_name);
}

function custom_title_tag(){
	if (get_field('title_tag')){
		the_field('title_tag');
	}else{
		wp_title('|', true, 'right');
		bloginfo('name');
	}
}

function custom_description_tag(){
	if (get_field('description_tag')){
		the_field('description_tag');
	}else{
		bloginfo('description');
	}
}
function wpdocs_get_paginated_links( $query ) {
    // When we're on page 1, 'paged' is 0, but we're counting from 1,
    // so we're using max() to get 1 instead of 0
    $currentPage = max( 1, get_query_var( 'paged', 1 ) );
 
    // This creates an array with all available page numbers, if there
    // is only *one* page, max_num_pages will return 0, so here we also
    // use the max() function to make sure we'll always get 1
    $pages = range( 1, max( 1, $query->max_num_pages ) );
 
    // Now, map over $pages and return the page number, the url to that
    // page and a boolean indicating whether that number is the current page
    return array_map( function( $page ) use ( $currentPage ) {
        return ( object ) array(
            "isCurrent" => $page == $currentPage,
            "page" => $page,
            "url" => get_pagenum_link( $page )
        );
    }, $pages );
}
function add_smartphone_cdn_attributes( $html, $handle ) {
    if ( 'smartphone' === $handle ) {
        return str_replace( "rel='stylesheet'", "rel='stylesheet' class='mc_css'", $html );
    }
    return $html;
}
add_filter( 'style_loader_tag', 'add_smartphone_cdn_attributes', 10, 2 );
add_filter('admin_body_class', 'wpse_320244_admin_body_class');

function wpse_320244_admin_body_class($classes) {
    global $post, $pagenow;

    // $pagenow contains current admin-side php-file
    // absint converts type to int, so we can use strict comparison
    if($pagenow === 'post.php' && (absint($post->ID) === 17 || absint($post->ID) === 15 || absint($post->ID) === 13)) {
        $classes .= ' home-page-area';
    }

    return $classes;
}
require get_parent_theme_file_path( '/func/core/assets.php' );
require get_parent_theme_file_path( '/func/core/walker.php' );
require get_parent_theme_file_path( '/func/core/breadcrum.php' );
require get_parent_theme_file_path( '/func/customizer/main.php' );
require get_parent_theme_file_path( '/func/widget/main.php' );


define('FACEBOOK_SDK_V4_SRC_DIR', __DIR__ . '/src/Facebook/');
require_once(__DIR__ . '/src/Facebook/autoload.php');
$fb = new Facebook\Facebook([
	'app_id' => '281083113175949',
	'app_secret' => '53187ad7861f5f90ae012e28082fe0d9',
	'default_graph_version' => 'v2.4',
]);
add_action( 'save_post', 'facebook_post', 10, 3 );
?>
```
