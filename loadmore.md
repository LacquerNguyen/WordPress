# loadmore WordPress
```php
add_action( 'wp_footer', 'my_action_javascript' ); // Write our JS below here

function my_action_javascript() { ?>
	<script type="text/javascript" >
	jQuery(document).ready(function($) {
       
       var page = 6;
       var post_count =  $('.p-note-list').data('count');
       var ajaxurl = " <?php echo admin_url('admin-ajax.php') ?>"
        $('#p-load-more').on('click',function() {      
            var data = {
                'action': 'my_action',
                'page': page
            };
            jQuery.post(ajaxurl, data, function(response) {
                $('.p-note-list').append(response);
                console.log(page)
                if(post_count == page){
                    $('#p-load-more').hide();
                }
                page++
            });
        })

	});
	</script> <?php
}


add_action( 'wp_ajax_my_action', 'my_action' );

function my_action() {
	global $wpdb; // this is how you get access to the 
	
	// render html loadmore

    $note_args = array(
        'post_type' => 'Note',
        'posts_per_page' => 2,
        'paged'     => $_POST['page'],
    );
    $note_args = new WP_Query($note_args)?>

    <?php if ($note_args->have_posts()) : ?>
        <?php while ($note_args->have_posts()) : $note_args->the_post();?>
        <div class="p-note-item">
            <a href="<?php the_permalink() ?>">
                <div class="p-note-image">
                    <img src="<?php the_post_thumbnail_url()?>" alt="" />
                </div>
                <div class="p-note-caption">
                    <span class="p-note-date"><?php  echo get_the_date(); ?></span>
                    <p class="p-note-detail"><?php the_title();?></p>
                </div>
            </a>
        </div>
    <?php endwhile; ?>
    <?php wp_reset_postdata(); ?>
    <?php endif;?>

	<?php wp_die(); ?>

<?php
}
?>
```
# html loadmore
```php
<?php
/*
    Template Name: Note page
*/
$note_args1 = array(
    'post_type' => 'Note',
    'posts_per_page' => -1,
);
$note_args1 = new WP_Query($note_args1);



$note_args = array(
    'post_type' => 'Note',
    'posts_per_page' => 10,
    'paged'     => $paged,
    'order'     => 'DESC',
);
$note_args = new WP_Query($note_args);
get_header();
?>
<main class="l-main l-note-page">
    <div class="container-ms">
        <div class="c-common-index">
            <h1 class="c-heading"><?php the_title();?></h1>
        </div>
        <div class="p-note-list" data-count="<?php echo ceil($note_args1->found_posts/2); ?>">
            <?php if ($note_args->have_posts()) : ?>
                <?php while ($note_args->have_posts()) : $note_args->the_post();?>
                <div class="p-note-item">
                    <a href="<?php the_permalink() ?>">
                        <div class="p-note-image">
                            <img src="<?php the_post_thumbnail_url()?>" alt="" />
                        </div>
                        <div class="p-note-caption">
                            <span class="p-note-date"><?php  echo get_the_date(); ?></span>
                            <p class="p-note-detail"><?php the_title();?></p>
                        </div>
                    </a>
                </div>
            <?php endwhile; ?>
            <?php wp_reset_postdata(); ?>
            <?php endif;?>
        </div>
        <p class="btn-readmore">
            <a id="p-load-more" href="javascript:void(0)">???????????????</a>
        </p>
    </div>
</main>


<?php get_footer(); ?>
```
