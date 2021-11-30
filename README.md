# wordpress_refer
wp complete query refer   ->   https://developer.wordpress.org/reference/classes/wp_query/
reference site link
1)db table refer site
   ->  (breif refer)   https://deliciousbrains.com/tour-wordpress-database/ 
   ->  (table structure)  https://usersinsights.com/wordpress-user-database-tables/  
   ->  (beginers refer)  https://blogvault.net/wordpress-database-schema/   
   
2)wordpress file directories refer site
   ->  https://www.wpbeginner.com/beginners-guide/beginners-guide-to-wordpress-file-and-directory-structure/ 
   
3)file directories structure
   ->    https://developer.wordpress.org/files/2014/10/Screenshot-2019-01-23-00.20.04.png
   
4)enqueu the css&js file in wp (function.php)
   -> https://hollypryce.com/enqueue/
   
5)wordpress query post(single.php) refer
   -> https://developer.wordpress.org/reference/classes/wp_query/
   
6)single.php query view code below
   <?php get_header();?>
<?php while ( have_posts() ) : the_post(); ?>
<div class="body">
	<div class="container">
		<div class="clear"></div>
		<div class="main">
			<div class="post content">
				<h1 class="page-title"><a href="<?php the_permalink(); ?>"><?php the_title();?></a></h1>

				<div class="content">
					<?php the_content(); ?>
				</div>
			</div>
		</div>
		<div class="clear"></div>
	</div>
</div>
<?php endwhile; ?>
<?php get_footer();?>


7)    query post sample code(all post data)
      -> $args = array(
      'post_type'=> 'post',
      'orderby'    => 'ID',
      'post_status' => 'publish',
      'order'    => 'DESC',
      'posts_per_page' => -1 // this will retrive all the post that is published 
      );
      $result = new WP_Query( $args );
      if ( $result-> have_posts() ) : ?>
      <?php while ( $result->have_posts() ) : $result->the_post(); ?>
      <?php the_title(); ?>   
      <?php endwhile; ?>
      <?php endif; wp_reset_postdata(); ?>
   
   Explain: while(condition){} ->  replace   ->while(condition) :(open bracket) &  endwhile;(close Bracket)    *same as all loops
   
   
   8)   add feauture img option in custom themes->post (section)
     function mytheme_post_thumbnails() {
    add_theme_support( 'post-thumbnails' );
}
add_action( 'after_setup_theme', 'mytheme_post_thumbnails' );

9)query post refer site
	->  https://awhitepixel.com/blog/query-posts-in-wordpress/

