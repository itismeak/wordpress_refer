# wordpress_refer
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
6)    query post sample code(all post data)
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

