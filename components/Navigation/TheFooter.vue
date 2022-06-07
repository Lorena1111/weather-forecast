<template>
  <footer>
    <div class="main-content">
      <div class="left box">
        <h2>O NAMA</h2>
        <div class="content">
          <p>Na našoj stranici možete pogledati vremensku prognozu za grad koji upišete. Ukoliko imate nekih dodatnih pitanja možete 
              nam se obratiti. </p>
        </div>
      </div>
      <div class="center box">
        <h2>ADRESA - TELEFON - E-MAIL</h2>
        <div class="content">
          <div>
            <span class="text">Ravnice 48, 10000 Zagreb</span>
          </div>
          <div class="tel">
            <span class="text">01 4565 666</span>
          </div>
          <div class="email">
            <span class="text">prognoza48@dhz.hr</span>
          </div>
        </div>
      </div>

      <div class="right box">
        <h2>KONTAKTIRAJTE NAS</h2>
        <div class="content">
          <form action="#">
            <div class="email">
              <div class="text">E-mail *</div>
              <input type="email" required />
            </div>
            <div class="poruka">
              <div class="text">Poruka *</div>
              <textarea cols="30" rows="3" required></textarea>
            </div>
            <div class="gumb">
              <a href="mailto:ljerbic@student.unipu.hr">
                <button>Pošalji</button>
              </a>
            </div>
          </form>
        </div>
      </div>
    </div>
    <div class="bottom">
      <center>
        <span> Created By
          <a href="#">Lorena</a> |
        </span>
        <span> &copy; {{ new Date().getFullYear() }} All rights reserved.</span>
      </center>
    </div>
  </footer>
</template>

<script>
export default {
  name: "TheFooter"
};
</script>
<style scoped>

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  color: white;
  font-family: Arial, Helvetica, sans-serif;
}

footer {
  width: 100%;
  background: blue;
}

.main-content {
  display: flex;
}

.main-content .box {
  flex-basis: 60%;
  padding: 15px 70px;
}

.box h2 {
  font-size: 18px;
  font-weight: bold;
}

.box .content {
  margin: 20px 10px 0 0;
  position: relative;
}

.box .content:before {
  position: absolute;
  content: "";
  top: -10px;
  height: 3px;
  width: 100%;
  background: gray;
}

.box .content:after {
  position: absolute;
  content: "";
  height: 3px;
  width: 50%;
  background: darkgray;
  top: -10px;
}

.left .content p {
  text-align: justify;
}

.left .content .social {
  margin: 20px 0 0 0;
}

.left .content .social a {
  padding: 0 2px;
}

.left .content .social a span i {
  height: 40px;
  width: 40px;
  background: darkslategray;
  line-height: 50px;
  text-align: center;
  font-size: 30px;
  border-radius: 5px;
}
.center .content .ion {
  font-size: 1.4375rem;
  background:darkslategray;
  height: 45px;
  width: 45px;
  line-height: 45px;
  text-align: center;
  border-radius: 50%;
  cursor: pointer;
}

.center .content .text {
  font-size: 16px;
  font-weight: 500;
  padding-left: 15px;
}

.center .content .tel {
  margin: 10px 0;
}

.right form .text {
  font-size: 16px;
  margin-bottom: 2px;
  color: gray;
}

.right form .poruka {
  margin-top: 10px;
}

.right form input,
.right form textarea {
  width: 100%;
  font-size: 16px;
  background: rgb(16, 27, 27);
  padding-left: 10px;
  border: 1px solid;
}

.right form input:focus,
.right form textarea:focus {
  outline-color: #073b5e;
}

.right form input {
  height: 35px;
}

.right form .gumb {
  margin-top: 10px;
}

.right form .gumb button {
  height: 40px;
  width: 100%;
  outline: none;
  background: black;
  font-size: 16px;
  font-weight: 500;
  cursor: pointer;
}

.right form .gumb button:hover {
  background: yellow;
  color:black;
  font-weight: bold;
}

.bottom center {
  padding: 5px;
  font-size: 14px;
  background: rgb(16, 27, 27);
}

.bottom center span {
  color: gray;
}

.bottom center a {
  color: blue;
  text-decoration: none;
}

.bottom center a:hover {
  text-decoration: underline;
  color:white;
}

@media screen and (max-width: 900px) {
  footer {
    position: static;
    bottom: 0px;
  }

  .main-content {
    flex-wrap: wrap;
    flex-direction: column;
  }

  .main-content .box {
    margin: 5px 0;
  }
}
</style>