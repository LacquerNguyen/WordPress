# WordPress
```php
<?php
/*
* Template Name: blog
*/
get_header();
$paged = (get_query_var('paged')) ? get_query_var('paged') : 1;

$blog_args = array(
  'post_type' => 'blog',
  'posts_per_page' => 1,
  'paged'     => $paged,
  // 'order'     => 'ASC',
);
$blog_posts = new WP_Query($blog_args);
?>
  <main id="main-content" class="page-content page-content--blog">
  <?php get_template_part('template-parts/blocks/banner-single');?>
    <section class="new-content-category">
      <div class="l-blog-container">
		<?php if ($blog_posts->have_posts()) : ?>
			<div class="latest-news">
			<?php while ($blog_posts->have_posts()) : $blog_posts->the_post();?>
				<div class="latest-news-inner">
					<div class="latest-news-image">
						<img src="<?php the_post_thumbnail_url()?>" alt="">
					</div>
					<div class="latest-news-caption">
						<p class="label-txt">NEW</p>
						<a class="news-ttl" href="<?php the_permalink() ?>"><?php the_title();?></a>
						<p class="news-day"><?php echo get_the_date(); ?></p>
					</div>
				</div>
			<?php endwhile; ?>
			</div>
		<?php endif;?>
      </div>
    </section>
  </main>
  <?php  get_footer();?>
```
