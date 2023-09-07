<template>
  <div>
    <h3 class="text-center mt-5">เกมเป่ายิงฉุบ</h3>

    <div class="box-game d-flex justify-content-center mt-5">
      <div class="user1">
        <h5 class="text-center">ผู้เล่น 1</h5>
        <img :src="player1ChoiceImage" alt="">
      </div>

      <div class="user2">
        <h5 class="text-center">ผู้เล่น 2</h5>
        <img :src="player2ChoiceImage" alt="">
      </div>
    </div>

    <div class="button mt-5 d-flex justify-content-center">
      <button class="btn btn-danger" @click="playGame"  data-bs-toggle="modal" data-bs-target="#exampleModal">เกมเป่ายิงฉุบ</button>
      <button @click="Resetgame" class="btn btn-success mx-4">เริ่มใหม่</button>
    </div>
  </div>

  <div class="score mt-3 d-flex justify-content-center">
    <div class="d-flex justify-content-center bg-success p-2 text-dark bg-opacity-25 ">

      <p class="fs-5"> คะแนน {{ scorePlayer1 }} : {{ scorePlayer2 }}</p>
    </div>
</div>




    <!-- Modal -->
<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h1 class="modal-title fs-5 text-center" id="exampleModalLabel">ผล</h1>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
      <p class="text-center fs-5 fw-bold text-danger">{{ resultMessage }}</p>
      <img :src="imagesplayer" width="300" height="300">
      </div>
     
    </div>
  </div>
</div>

</template>

<script>
export default {
  data() {
    return {
      choices: ['ค้อน', 'กระดาษ', 'กรรไกร'],
      player1Choice: '',
      player2Choice: '',
      player1ChoiceImage: 'https://scontent.fcnx2-1.fna.fbcdn.net/v/t39.30808-6/316666599_1733639837029942_2312109162028137071_n.jpg?_nc_cat=101&ccb=1-7&_nc_sid=1b51e3&_nc_ohc=fm1POmwkQL4AX_dfIoO&_nc_ht=scontent.fcnx2-1.fna&oh=00_AfDio_mpqBtJuPbDRyBE-FcMpFS55GlhVGKkZso7ABfjLg&oe=64FED159', // รูปเริ่มต้น
      player2ChoiceImage: 'https://scontent.fcnx2-1.fna.fbcdn.net/v/t39.30808-6/296733417_1410703336065987_6754551621006898346_n.jpg?_nc_cat=110&ccb=1-7&_nc_sid=1b51e3&_nc_ohc=GYD6SsFn8hQAX8WIVI6&_nc_ht=scontent.fcnx2-1.fna&oh=00_AfD1RO6qF7x6CShq-brKtbeCiQuXwTjrZl8chCpAn0l7NQ&oe=64FF03D0', // รูปเริ่มต้น
      resultMessage: '',
      scorePlayer1: 0, // คะแนนผู้เล่น 1
      scorePlayer2: 0,  // คะแนนผู้เล่น 2
      
    };
  },
  methods: {
    playGame() {
      const randomIndex1 = Math.floor(Math.random() * this.choices.length);
      const randomIndex2 = Math.floor(Math.random() * this.choices.length);

      this.player1Choice = this.choices[randomIndex1];
      this.player2Choice = this.choices[randomIndex2];

      this.player1ChoiceImage = this.getImagePath(this.player1Choice);
      this.player2ChoiceImage = this.getImagePath(this.player2Choice);

      this.calculateWinner();
    },
    getImagePath(choice) {
      if (choice === 'ค้อน') {
        return 'https://dx.lnwfile.com/_/dx/_raw/cp/z3/u1.jpg';
      } else if (choice === 'กระดาษ') {
        return 'https://static.wixstatic.com/media/249f63_a90293220fb44aa297ad70e06182ed46~mv2.png/v1/fill/w_625,h_469,al_c,q_85,usm_0.66_1.00_0.01,enc_auto/249f63_a90293220fb44aa297ad70e06182ed46~mv2.png';
      } else if (choice === 'กรรไกร') {
        return 'https://image.makewebeasy.net/makeweb/m_1920x0/e8kyJI8FV/scissors/A300.jpg?v=202305101549';
      }
    },
    calculateWinner() {
      if (this.player1Choice === this.player2Choice) {
        this.resultMessage = 'เสมอ';
        this.imagesplayer = "https://scontent.fcnx2-1.fna.fbcdn.net/v/t1.6435-9/82299750_2503692733234836_3398054451011911680_n.jpg?_nc_cat=107&ccb=1-7&_nc_sid=8bfeb9&_nc_ohc=WGGoGye6JcgAX_N7W6b&_nc_ht=scontent.fcnx2-1.fna&oh=00_AfCWvqYWI6Qn0wA70Tg22Obk_BFW0SfJeOTmUvO44yO3jQ&oe=65211559"
      } else if (this.player1Choice ==="ค้อน" && this.player2Choice === "กรรไกร" || 
      this.player1Choice ==="กรรไกร" && this.player2Choice === "กระดาษ" ||
       this.player1Choice ==="กระดาษ" && this.player2Choice === "ค้อน"  ) {
        this.resultMessage = 'ผู้เล่น 1 ชนะ';
        this.scorePlayer1++; // เพิ่มคะแนนผู้เล่น 1
        this.imagesplayer ='https://scontent.fcnx2-1.fna.fbcdn.net/v/t39.30808-6/316666599_1733639837029942_2312109162028137071_n.jpg?_nc_cat=101&ccb=1-7&_nc_sid=1b51e3&_nc_ohc=fm1POmwkQL4AX_dfIoO&_nc_ht=scontent.fcnx2-1.fna&oh=00_AfDio_mpqBtJuPbDRyBE-FcMpFS55GlhVGKkZso7ABfjLg&oe=64FED159';
      } else {
        this.resultMessage = 'ผู้เล่น 2 ชนะ';
        this.scorePlayer2++; // เพิ่มคะแนนผู้เล่น 2
        this.imagesplayer ='https://scontent.fcnx2-1.fna.fbcdn.net/v/t39.30808-6/296733417_1410703336065987_6754551621006898346_n.jpg?_nc_cat=110&ccb=1-7&_nc_sid=1b51e3&_nc_ohc=GYD6SsFn8hQAX8WIVI6&_nc_ht=scontent.fcnx2-1.fna&oh=00_AfD1RO6qF7x6CShq-brKtbeCiQuXwTjrZl8chCpAn0l7NQ&oe=64FF03D0';
        
      }
    },
      Resetgame(){
        window.location.reload(); // รีเซ็ตหน้าเว็บ
      }
    
    }
  
};
</script>

<style>
.user1,.user2{
  border: 2px solid rgb(227, 12, 12);
  padding: 50px;
}
.box-game img{
  width: 250px;
  height: 250px;
}


</style>