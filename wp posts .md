# lấy dữ liệu posts wp
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
    <?php if (have_posts()) : ?>
        <?php while (have_posts()) : the_post(); 
        ?> 
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
                <div class="detail-title">
                    <p>言語学習のゴールは、完璧な言語を話すことではない。</p>
                </div>
                <div class="detail-description">
                    <?php the_content(); ?>
                </div>
            </div>
        </div>
        <?php endwhile; ?>
    <?php endif; ?>
