# WordPress
```php
$total_pages = $news_args->max_num_pages;
            if ($total_pages > 1) {
            ?>
                <div class="l-pagination">
                    <nav class="navigation pagination">
                        <div class="nav-links">
                            <?php
                            $big = 999999999;
                            echo paginate_links(array(
                                'base' => str_replace( $big, '%#%', esc_url( get_pagenum_link( $big ) ) ),
                                'format' => 'page/%#%',
                                'current' => $paged,
                                'total' => $total_pages,
                                'next_text'          => __( '>' ),
                                'prev_text'          => __( '<' ),
                                'end_size'           => 0,
                                'mid_size'           => 1,
                            ));
                            ?>
                        </div>
                    </nav>
                </div>

            <?php } ?>
```
