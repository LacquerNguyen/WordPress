# Header
```html
<!DOCTYPE html>
<html <?php language_attributes(); ?>>
<head prefix="og: http://ogp.me/ns# fb: http://ogp.me/ns/fb# article: http://ogp.me/ns/article#">

    <meta charset="<?php bloginfo( 'charset' ); ?>">
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <meta name="format-detection" content="telephone=no">
    <?php wp_head(); ?>
</head>
<body>
        <?php if(is_front_page() || is_home()): ?>
         <div id="app" class="page-wrapper p-top">
            <header class="l-header">
            <?php else: ?>
            <div id="app" class="page-wrapper">
            <header class="l-header header-index">
                <div class="l-container--wrapper">
                    <a href="/">
                        <p class="p-top_main_logo"><img src="<?php echo get_stylesheet_directory_uri(); ?>/assets/images/common/logo.svg" alt="crosslimit" /></p>
                    </a>
                </div>
            <?php endif; ?>
            <div class="p-menu">
                <p class="p-menu_btn">
                    <button class="p-menu_btnMenu"><span class="icon-hamburger"><span></span><span></span><span></span></span></button>
                </p>
                <div class="l-menusp">
                    <ul>
                        <?php wp_nav_menu(array(
                            'theme_location' => '', 
                            'menu_id' => 'menu', 
                            'menu_class' => 'menu'
                        )) ?>
                    </ul>
                </div>
                <p class="p-menu_scroll">
                    <img src="<?php echo get_stylesheet_directory_uri(); ?>/assets/images/common/scroll.svg" alt="SCROLL" />
                    <span class="p-scroll-down"></span>
                </p>
            </div>
        </header>
```
