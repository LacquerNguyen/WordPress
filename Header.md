# Header
```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" <?php language_attributes(); ?>>

<head>
	<meta http-equiv="Content-type" content="text/html;charset=UTF-8">
	<meta name="format-detection" content="telephone=no">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">

	<title><?php custom_title_tag(); ?></title>
	<meta name="description" content="<?php custom_description_tag(); ?>" />
	<?php if (get_field('keyword')) { ?>
		<meta name="keyword" content="<?php the_field('keyword'); ?>" />
	<?php } ?>
	<meta name="robots" content="index,follow">
	<link rel="canonical" href="<?php global $wp;
								echo home_url($wp->request); ?>" />
	<meta property="og:locale" content="<?php echo apply_filters('wpml_current_language', NULL); ?>" />
	<meta property="og:type" content="website" />
	<meta property="og:title" content="<?php custom_title_tag(); ?>" />
	<meta property="og:description" content="<?php custom_description_tag(); ?>" />
	<meta property="og:url" content="<?php echo home_url($wp->request); ?>" />
	<meta property="og:site_name" content="<?php custom_title_tag(); ?>" />
	<?php
	$og_image = '';
	if (get_field('image_tag')) {
		$og_image = get_field('image_tag');
	} else {
		if (is_single() || is_page()) {
			$og_image = get_the_post_thumbnail_url(get_the_ID(), 'full');
		}
	}
	if ($og_image) {
	?>
		<meta property="og:image" content="<?php echo $og_image; ?>" />
	<?php } ?>
	<meta name="twitter:card" content="summary_large_image">


	<link rel="shortcut icon" href="<?php bloginfo('template_url'); ?>/shared/images/favicon/favicon.ico" type="image/x-icon">
	<link rel="icon" href="<?php bloginfo('template_url'); ?>/shared/images/favicon/favicon.ico" type="image/x-icon">
	<link rel="apple-touch-icon" href="<?php bloginfo('template_url'); ?>/shared/images/favicon/apple-touch-icon-precomposed.png">
	<link rel="apple-touch-icon-precomposed" href="<?php bloginfo('template_url'); ?>/shared/images/favicon/apple-touch-icon-precomposed.png">
	<?php wp_head(); ?>
	<!-- Global site tag (gtag.js) - Google Analytics -->
	<script async src="https://www.googletagmanager.com/gtag/js?id=UA-121630851-1"></script>
	<script>
		window.dataLayer = window.dataLayer || [];

		function gtag() {
			dataLayer.push(arguments);
		}
		gtag('js', new Date());
		gtag('config', 'UA-121630851-1');
		//window['ga-disable-UA-121630851-1'] = true; //Disable google analytics
	</script>
</head>

<body <?php
		$accesibility_page = get_lang(69, 71, 73);
		$search_page = get_lang(75, 77, 79);
		$addition_class = 'no_javascript';
		if (is_home() || is_front_page()) {
			$addition_class .= ' format_top';
		} else {
			$addition_class .= ' format_free';
		}
		body_class($addition_class);
		?>>
	
	<div id="fb-root"></div>
	<script async defer crossorigin="anonymous" src="https://connect.facebook.net/vi_VN/sdk.js#xfbml=1&version=v7.0" nonce="9PvITlho"></script>
	<div id="tmp_wrapper" class="<?php echo_lang('lang_jp', 'lang_vn', 'lang_en') ?>">
		<noscript>
			<p><?php show_string_lang('no_js'); ?></p>
		</noscript>
		<p><a href="#tmp_honbun" class="skip"><?php show_string_lang('honbun'); ?></a></p>
		<?php if (is_home() || is_front_page()) echo '<div id="fullpage"><div class="section_area wrap_firstview" id="section_firstview">'; ?>
		<div id="tmp_header">
			<div class="container">
				<div id="tmp_hlogo">
					<?php if (is_home() || is_front_page()) { ?>
						<h1><span><?php echo_lang('オフショア開発支援はGDITにお任せください Global Design IT Co., Ltd.', 'Hãy để GDIT hỗ trợ bạn việc phát triển offshore. Global Design IT Co., Ltd.', 'Let GDIT have the honor of supporting you on offshore development. Global Design IT Co., Ltd.'); ?></span></h1>
					<?php } else { ?>
						<p><a href="<?php bloginfo('url'); ?>"><span><?php echo_lang('オフショア開発支援はGDITにお任せください Global Design IT Co., Ltd.', 'Hãy để GDIT hỗ trợ bạn việc phát triển offshore. Global Design IT Co., Ltd.', 'Let GDIT have the honor of supporting you on offshore development. Global Design IT Co., Ltd.') ?></span></a></p>
					<?php } ?>
				</div>
				<div id="tmp_header_cnt">
					<div id="tmp_setting_wrap">
						<div id="tmp_means">
							<ul>
								<li class="setting_func"><a href="<?php echo get_permalink($accesibility_page); ?>"><?php echo get_the_title($accesibility_page); ?></a></li>
							</ul>
						</div>
						<ul id="tmp_hnavi_s">
							<li id="tmp_hnavi_lmenu"><a href="javascript:void(0);"><span><?php show_string_lang('search'); ?></span></a></li>
							<li id="tmp_hnavi_rmenu">
								<a href="javascript:void(0);" class="sma_menu_open"><span class="menu_icon">&nbsp;</span><span class="menu_text"><?php echo_lang('メニュー', 'Menu', 'Menu'); ?></span></a>
							</li>
						</ul>
						<div class="switch_language">
							<ul class="language_list_group">
								<li class="dropdown_language">
									<?php $langs = icl_get_languages('skip_missing=0&orderby=id'); ?>
									<a class="btn_language" href="javascript:void(0)"> <img src="<?php bloginfo('template_url'); ?>/shared/images/header/<?php echo ICL_LANGUAGE_CODE; ?>.png" alt="" height="16" width="24" /></a>
									<ul class="dropdown_menu_language">
										<?php
										foreach ($langs as $key => $lang) {
											if (!$lang['active']) {
										?>
												<li>
													<a class="btn_language" href="<?php echo $lang['url'] ?>"><img src="<?php bloginfo('template_url'); ?>/shared/images/header/<?php echo $key ?>.png" height="16" width="24" alt="" /></a>
												</li>
										<?php }
										} ?>
									</ul>
								</li>
							</ul>
						</div>
					</div>
					<?php
					wp_nav_menu(array(
						'theme_location' => 'top',
						'container_class' => 'gnavi',
					))
					?>
				</div>
			</div>
		</div>
		<div id="tmp_sma_menu">
			<div class="wrap_sma_sch" id="tmp_sma_lmenu">
				<div id="tmp_sma_search">
					<form id="tmp_sma_gsearch" action="<?php echo get_permalink($search_page) ?>" method="GET" name="tmp_sma_gsearch">
						<div class="wrap_sch_box">
							<p class="sch_ttl"><label for="tmp_sma_query"><?php echo_lang('サイト内検索', 'Tìm kiếm trên trang', 'Search in site') ?></label></p>
							<p class="sch_box"><input type="text" size="31" name="search_key" id="tmp_sma_query" /></p>
						</div>
						<div class="wrap_sch_box">
							<p class="sch_select"></p>
							<p class="sch_btn"><input type="submit" value="<?php show_string_lang('search'); ?>" id="tmp_sma_func_sch_btn" /></p>
						</div>
					</form>
					<p class="view_btn">
						<a href="#"></a>
					</p>
				</div>
				<p class="close_btn"><a href="javascript:void(0);"><span><?php show_string_lang('close'); ?></span></a></p>
			</div>
			<div class="wrap_sma_sch" id="tmp_sma_rmenu">
				<p class="close_btn"><a href="javascript:void(0);"><span><?php show_string_lang('close'); ?></span></a></p>
			</div>
		</div>
		<!--end header-->
    ```
