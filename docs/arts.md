<style>
.art-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
  gap: 16px;
  margin-top: 20px;
}

.art-card {
  text-align: center;
  font-size: 0.9rem;
}

.art-card img {
  width: 100%;
  aspect-ratio: 1 / 1;
  object-fit: cover;
  border-radius: 10px;
  transition: transform 0.3s ease;
}

.art-card img:hover {
  transform: scale(1.05);
}

.art-caption {
  margin-top: 6px;
  color: #555;
}
</style>

<div class="art-grid">

  <div class="art-card">
    <img src="/assets/images/art4.jpeg" alt="Luffy">
    <div class="art-caption"><b>Luffy</b><br>Never give up!</div>
  </div>

  <div class="art-card">
    <img src="/assets/images/art6.jpeg" alt="Kokushibo">
    <div class="art-caption"><b>Kokushibo</b><br>Drew this during class XD</div>
  </div>

  <div class="art-card">
    <img src="/assets/images/art5.jpeg" alt="RDJ">
    <div class="art-caption"><b>RDJ</b><br>Sketch was good, pen ruined it 😭</div>
  </div>

  <div class="art-card">
    <img src="/assets/images/art9.jpeg" alt="Tanjiro x Kanao">
    <div class="art-caption"><b>Tanjiro × Kanao</b><br>The famous coin flip scene</div>
  </div>

  <div class="art-card">
    <img src="/assets/images/art1.jpeg" alt="Nezuko x Zenitsu">
    <div class="art-caption"><b>Nezuko & Zenitsu</b><br>Nezuko worried ❤️</div>
  </div>

  <div class="art-card">
    <img src="/assets/images/art7.jpeg" alt="Vayalar">
    <div class="art-caption"><b>Vayalar</b><br>Local poet</div>
  </div>

  <div class="art-card">
    <img src="/assets/images/art8.jpeg" alt="O. N. V. Kurup">
    <div class="art-caption"><b>O. N. V. Kurup</b><br>Local poet</div>
  </div>

  <div class="art-card">
    <img src="/assets/images/art3.jpeg" alt="Friendship">
    <div class="art-caption"><b>Friendship</b></div>
  </div>

</div>
