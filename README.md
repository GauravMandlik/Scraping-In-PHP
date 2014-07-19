Scraping-In-PHP
===============

I have done a scraping using a PHP scripting language to scrape a data from the site

My Code Is ...



<html>
	<head>
	<meta http-equiv="Content-Type" content="text/html; charset=utf-8">

<?php
	include "simple_html_dom.php";
	function file_get_contents_curl($url)
	{
		$ch = curl_init();
		curl_setopt($ch, CURLOPT_HEADER, 0);
		curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
		curl_setopt($ch, CURLOPT_URL, $url);
		curl_setopt($ch, CURLOPT_FOLLOWLOCATION, 1);

		$data = curl_exec($ch);
		curl_close($ch);

		return $data;
	}
	
	$html = str_get_html(file_get_contents_curl("http://www.divyabhaskar.co.in/sports/"));	
	/*foreach ($html->find('div[class=cri_flicker]') as $element) {
    $links = $element->find('a');
            foreach ($links as $link) {
                echo $link->href.'<br>';
            }
        }
	*/
	
	foreach($html->find('div[class=cri_flicker]') as $key => $info)
	{
		echo ($key + 1).'. '.$info->plaintext."<br />\n";
	}
	
	$doc = new DOMDocument();
	@$doc->loadHTML($html);
	//echo "$html";
	
?>
	</head>
</html>
