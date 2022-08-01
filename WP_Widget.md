# WordPress
```php
class Team_Member extends WP_Widget
{
    function __construct()
    {
        parent::__construct(
            'team_member',
            'Team Member',
            array('description'  =>  'Widget display Team Member')
        );
    }


    function form($instance)
    {


        $default = array(
            'title' => 'Widget Title',
        );
        $instance = wp_parse_args((array) $instance, $default);
    }


    function update($new_instance, $old_instance)
    {
        $instance = $old_instance;
        return $instance;
    }


    function widget($args, $instance)
    {
        extract($args);


        echo $before_widget;
        $team_query = new WP_Query('post_type=department&posts_per_page=-1&orderby=date&order=ASC');


        if ($team_query->have_posts()) :
            echo '<div
                class="owl-carousel team-carousel"
                data-loop="true"
                data-margin="5"
                data-responsive-xs="1"
                data-responsive-sm="2"
                data-responsive-md="2"
                data-responsive-lg="3"
              >';
            while ($team_query->have_posts()) :
                $team_query->the_post(); ?>


                <div class="owl-carousel-item team excerpt-none">
                    <div class="vertical-item team-item text-center">
                        <div class="item-media">
                            <img width="800" height="796" src="<?php the_post_thumbnail_url('full'); ?>" alt="" />
                            <div class="media-links">
                                <a class="abs-link" href="<?php echo get_the_permalink(); ?>"></a>
                            </div>
                        </div>

                        <div class="item-content mt-35">
                            <h5 class="mb-2 fw-400">
                                <a href="<?php echo get_the_permalink(); ?>"><?php echo get_the_title(); ?></a>
                            </h5>
                            <p class="team-position text-uppercase letter-sp-small fs-14">
                                <?php the_field('position'); ?>
                            </p>

                            <div class="team-excerpt">
                                Interdum et malesuada fames ac ante ipsum primis in faucibus. .
                            </div>
                            <!-- eof social icons -->
                        </div>
                    </div>
                    <!-- eof .vertical-item -->
                </div>


<?php endwhile;
            echo "</div>";
        endif;
        echo $after_widget;
    }
}


add_action('widgets_init', 'create_team_member');
function create_team_member()
{
    register_widget('Team_Member');
}

```
