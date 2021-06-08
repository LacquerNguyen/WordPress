# WordPress
```php
<?php
/*
* Template Name: Blog single page
*/
$paged = (get_query_var('paged')) ? get_query_var('paged') : 1;
$blog_args = array(
    'post_type' => 'blog',
    'posts_per_page' => 4,
    'paged'     => $paged,
    // 'order'     => 'ASC',
);
$blog_posts = new WP_Query($blog_args);
get_header();
?> 
<?php get_template_part('template-parts/blocks/badge');?>

<main id="main-content" class="page-content page-content--single_blog">
    <?php if (have_posts()) : ?>
        <?php while (have_posts()) : the_post(); ?> 
        <div class="latest-news blog-single">
            <div class="latest-news-inner">
                <div class="latest-news-image">
                    <img src="<?php the_post_thumbnail_url()?>" alt="">
                </div>
                <div class="latest-news-caption">
                    <p class="label-txt">NEW</p>
                    <p class="news-ttl"><?php the_title(); ?><p>
                    <p class="news-day"><?php the_date();?></p>
                </div>
            </div>
        </div>
        <div class="blog-detail">
            <div class="l-container-100">
                <div class="detail-description">
                    <?php the_content(); ?>
                </div>
            </div>
        </div>
        <?php endwhile; ?>
    <?php endif; ?>
    <div class="orther-blog">
        <div class="l-blog-container">
            <h2>OTHER BLOG</h2>
        <?php if ($blog_posts->have_posts()) : ?>
            <div class="new-posts-list">
                <?php while ($blog_posts->have_posts()) : $blog_posts->the_post();?>
                    <div class="new-posts-item">
                        <a href="<?php the_permalink() ?>">
                            <div class="new-posts-content">
                                <div class="new-posts-image">
                                    <img src="<?php the_post_thumbnail_url()?>" alt="" />
                                </div>
                                <div class="new-posts-caption">
                                    <p class="txt-ttl"><?php the_title();?></p>
                                    <p class="txt-day"><?php echo get_the_date(); ?></p>
                                </div>
                            </div>
                        </a>
                    </div>
                <?php endwhile; ?>
            </div>
            <div class="c-btn--readMore">
                <a class="c-btn--readMore_inner" href="<?php echo home_url(); ?>/blog">BACK TO PAGE</a>
            </div>
            <?php endif;?>
        </div>
    </div>
</main>
<?php  get_footer();?>
```
