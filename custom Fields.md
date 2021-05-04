# lấy dữ liệu custom Fields.md
``php
<?php 
    $people_args = array(
        'post_type' => 'people',
        // 'offset' => 2, 
        'posts_per_page' => 2,
        'paged'     => $paged,
        // 'order'     => 'ASC',
    );
    $people_posts = new WP_Query($people_args);
?>
<?php if ($people_posts->have_posts()) : ?>
        <?php while ($people_posts->have_posts()) : $people_posts->the_post(); ?>
            <li>
                <div class="member-infor-item">
                    <a href="<?php the_permalink() ?>">
                        <div class="member-image">
                            <img src="<?php the_field('image'); ?>" alt="">
                        </div>
                        <p class="member-name"><?php the_field('name'); ?><p>
                        <p class="member-position"><?php the_field('position'); ?><p>
                        <p class="member-description"><?php the_field('description'); ?><p>
                    </a>
                </div>
                <div class="c-btn--readMore">
                    <a href="<?php the_permalink() ?>" class="c-btn--readMore_inner">READ MORE</a>
                </div>
            </li>
        <?php endwhile; ?>
    <?php wp_reset_postdata(); ?>
<?php endif;?>
```
