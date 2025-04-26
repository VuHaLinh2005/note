<style>
  :root {
    --main-color: #ff0000; /* tạo biến,*/
  }
  
  .box {
    background: var(--main-color);/*use biến
  }
  /*root đại diện thư mục gốc (thẻ <html>)  tạo biến ở đây coi như là toàn cục (vì html là gốc-rộng nhất) 
</style>
<div class="box">Hộp màu</div>
<script>
  // Đổi màu sang xanh khi nhấn
  document.querySelector('.box').addEventListener('click', () => {
    document.documentElement.style.setProperty('--main-color', '#0000ff');
  });
</script>


