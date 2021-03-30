# WordPress
```html
	function echo_link($url,$link,$class){
		if ($link){
			echo '<li class="'.$class.'">';
			if ($url) echo '<a href="'.$link.'" target="_blank">';
			echo '<img src="'.$url.'" alt="" width="32" height="32" />';
			if ($url) echo '</a>';
		}
	}
?>
	<div id="tmp_footer">
		<div class="container">
			<div class="pnavi">
				<p class="ptop"><a href="#tmp_header"><?php show_string_lang('back_to_top') ?></a></p>
			</div>
			<div class="footer_cnt">
				<div class="footer_logo">
					<p><a href="<?php bloginfo('url') ?>"><span><?php echo_lang('オフショア開発支援はGDITにお任せください Global Design IT Co., Ltd.','Hãy để GDIT hỗ trợ bạn việc phát triển offshore. Global Design IT Co., Ltd.','Let GDIT have the honor of supporting you on offshore development. Global Design IT Co., Ltd.'); ?></span></a></p>
				</div>
				<address>
					<p class="footer_address"><?php the_field_multilang('info--address'); ?></p>
<?php $phones = get_field_multilang('info--phone'); 
if ($phones && count($phones)){
	foreach($phones as $key => $phone){ 
		echo '<p class="phone_number">'.$phone['phone'].'</p>';
	}
}
?>
				</address>
				<div class="social_links">
					<ul>
						<li class="social_isms">
							<img src="<?php the_field_multilang('info--logo-isms') ?>" alt="ISMS" />
						</li>
						<?php
						echo_link(get_bloginfo('template_url').'/shared/images/icon/icon_facebook.svg',get_field_multilang('info--facebook-link'),'social_fb');
						echo_link(get_bloginfo('template_url').'/shared/images/icon/icon_linkedin.svg',get_field_multilang('info--linkedin-link'),'social_in');
						?>
					</ul>
				</div>
			</div>
			<?php 
				wp_nav_menu(array(
					'theme_location' => 'footer',
					'container_class' => 'fnavi_group',
					'menu_class' => 'fnavi'
				))
			?>
			<div class="block_facebook">
				<div class="fb-page" data-href="https://www.facebook.com/globaldesignit.vn/?ref=br_rs" data-tabs="timeline" data-width="329" data-height="207" data-small-header="true" data-adapt-container-width="true" data-hide-cover="false" data-show-facepile="true">
					<blockquote cite="https://www.facebook.com/globaldesignit.vn/?ref=br_rs" class="fb-xfbml-parse-ignore"><a href="https://www.facebook.com/globaldesignit.vn/?ref=br_rs">GLOBAL DESIGN IT</a></blockquote>
				</div>
			</div>
		</div>
		<div class="copyright_group">
			<p class="copyright" lang="en" xml:lang="en">&copy; 2020 GLOBAL DESIGN IT Co,LTD.</p>
		</div>
	</div>
	<?php if (is_home() || is_front_page()) echo '</div></div>'; ?>
</div>
<!--end wrapper-->
</body>

</html>
<?php wp_footer(); ?>
</body>
</html>
```
