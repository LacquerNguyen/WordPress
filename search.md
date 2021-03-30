# WordPress
```html
<?php
    $search_key = $_GET['search_key'];
    function get_ex( $id, $count ) {
        $content_post = get_post($id);
        $excerpt = $content_post->post_content;
        $excerpt = apply_filters('the_content', $excerpt);
        $excerpt = str_replace(']]>', ']]&gt;', $excerpt);
        $excerpt = strip_tags($excerpt);
        $excerpt = substr($excerpt, 0, $count);
        return $excerpt.'...';
    }
 ?>
<?php get_header(); ?>
<div class="page_banner">
    <div class="banner_img">
        <p><?php the_post_thumbnail('full'); ?></p>
    </div>
    <div class="container">
        <div id="tmp_pankuzu">
            <p class="pankuzu_white">
                <?php get_breadcrum(); ?>
            </p>
        </div>
        <h1 class="big_ttl"><?php the_title() ?></h1>
    </div>
</div>
<p id="tmp_honbun" class="skip"><?php show_string_lang('honbun_target'); ?></p>
<div id="tmp_wrap_main" class="column_cnt">
    <div id="tmp_main">
        <div class="col_main">
            <div id="tmp_contents" style="padding-bottom: 50px">
                <div class="container development_caption">
                    <?php $search_query = new WP_Query( 
                        array( 
                                'post_type' => array('post', 'development','page'),
                                'post__not_in' => array(2837, 2870, 2872),
                                's' => $search_key, 
                            ) 
                        ); 
                        $searchArr[] = array();
                    ?>
                    <?php 
                    if ($search_query->have_posts()) { while ($search_query->have_posts()) : $search_query->the_post();
                        if ( is_page() && $post->post_parent ) {
                            array_push($searchArr, $post->post_parent);
                        } else {
                            array_push($searchArr, $post->ID);
                        }
                        $searchArr = array_unique($searchArr);
                    ?>
                    <?php endwhile;?>
                    <?php wp_reset_query(); ?>
                    <?php } else { ?> 
                        <div id="tmp_not_found">
                            <h3 style="border-bottom: none"><?php echo_lang('該当結果が見つかりませんでした。','Không tìm thấy kết quả.','No results were found.'); ?></h3>
                            <div class="see_more">
                                <a href="<?php bloginfo('url'); ?>"><?php echo_lang('トップページに戻る','Trở về trang chủ','Back Home'); ?></a>
                            </div>
                        </div>
                    <?php }
                        foreach ($searchArr as $i => $value) { 
                            if($i > 0) {
                        ?>
                            <p class="development_heading">
                                <a href="<?php the_permalink($value) ?>"><?php echo get_the_title($value) ?></a>
                            </p>
                            <p class="development_intro"><?php echo get_ex($value, 255); ?></p>
                    <?php
                            }
                        }
                    ?>
                </div>
            </div>
        </div>
    </div>
</div>

<?php get_footer(); ?>
```
