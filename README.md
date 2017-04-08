# Codeigniter Contact Form

## Add to Controller Code : 

	// İletişim Formu için..
	if(isset($_POST) && !empty($_POST)){
	    //Formdakileri al reis
	    $adsoyad = $this->input->post('adsoyad');
	    $sirketadi = $this->input->post('sirketadi');
	    $eposta = $this->input->post('eposta');
	    $telefon = $this->input->post('telefon');
	    $mesaj = $this->input->post('mesaj');

	    // Gönderilecek olan mail adresi
	    $to_email = 'mail@siteadi.com';

	    // Mail bilgileri
	    $config['protocol'] = 'smtp';
	    $config['smtp_crypto'] = 'ssl';
	    $config['smtp_host'] = 'smtp.yandex.com.tr';
	    $config['smtp_port'] = '465';
	    $config['smtp_user'] = 'mail@siteadi.com';
	    $config['smtp_pass'] = 'sifre';
	    $config['mailtype'] = 'html';
	    $config['charset'] = 'utf-8';
	    $config['wordwrap'] = TRUE;
	    $config['newline'] = "\r\n";
	    
	    $this->load->library('email', $config);
	    $this->email->initialize($config);   

	    $icerik = 'Ad Soyad : '.$adsoyad.'<br/>Şirket Adı : '.$sirketadi.'<br/>'.'Mail Adresi : '.$eposta.'<br/>'.'Telefon : '.$telefon.'<br/>'.' Mesaj : '.$mesaj.'<br/><br/> Bu mail https://www.nirvanayazilim.com/ adresinden gönderilmiştir.';                   

	    //Mail bilgileri
	    $this->email->from('mail@siteadi.com', 'Site_Adı');
	    $this->email->to($to_email);
	    $this->email->subject('İletişim Formu');
	    $this->email->message($icerik);

	    if ($this->email->send()){
	        // gönderildi
	        $this->session->set_flashdata('mesaj','<script type="text/javascript">swal("Gönderildi", "Mesajınız başarılı şekilde gönderilmiştir. En kısa sürede size geri dönüş yapılacaktır.", "success")</script>');
	    }else{
	        //hata
	        $this->session->set_flashdata('mesaj','<script type="text/javascript">swal("Hata !", "Mesajınız teknik bir hatadan dolayı gönderilemedi.", "error")</script>');
	    }
	}
	$data["uyari"] = $this->session->flashdata('mesaj');
  
  
  ## Add to View Code :
```
<script src="<?php echo base_url("assets/front/sweet/"); ?>sweetalert.min.js"></script>
<link rel="stylesheet" type="text/css" href="<?php echo base_url("assets/front/sweet/"); ?>sweetalert.css">
<?php if(!empty($uyari)){echo $uyari;} ?>
```

## Upload assets folder to Sweeat Alert file :
