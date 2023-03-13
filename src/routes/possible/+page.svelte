<!-- App.svelte -->
<script>
    export let title = 'Lyric Generator';
  </script>
  
  <head>
    <title>{title}</title>
  </head>
  
  <header>
    <div class="header-container">
      <div class="header-wrapper">
        <h1 class="title">{title}</h1>
        <p class="subtitle">Lyrics generated with AI</p>
      </div>
    </div>
  </header>
  
  <main class="container">
    <div class="ad-container">
      <!-- ad code here -->
    </div>
  
    <section class="main-section">
      <h2 class="main-title">Do you struggle with writing lyrics for your songs? Look no further than Lyric Generator!</h2>
      <p>Our powerful AI algorithm will help you create catchy and meaningful lyrics in no time. Simply input a few keywords, and our software will do the rest.</p>
    </section>
  
    <section class="main-section">
      <h2 class="subsection-title">How it Works</h2>
      <ol>
        <li>Enter keywords related to your song.</li>
        <li>Choose a genre or style.</li>
        <li>Click the "Generate Lyrics" button.</li>
        <li>Enjoy your new lyrics!</li>
      </ol>
    </section>
  
    <div class="ad-container">
      <!-- ad code here -->
    </div>
  
    <section class="main-section">
      <h2 class="subsection-title">Benefits of Using Lyric Generator</h2>
      <ul>
        <li><h3 class="sub-section-title">Save time and effort</h3>Never again will you have to struggle to come up with the perfect words to match your melody. Lyric Generator does the hard work for you, leaving you free to focus on what really matters - making music!</li>
        <li><h3 class="sub-section-title">Improve the quality of your lyrics</h3>Our AI algorithm takes your input and generates lyrics that are not only catchy but also meaningful. Say goodbye to generic and uninspired lyrics, and hello to truly original and impactful songwriting.</li>
        <li><h3 class="sub-section-title">Explore new topics and themes</h3>Lyric Generator provides a wealth of inspiration and ideas for your songwriting. Whether you're looking to write a love ballad or a protest anthem, our software can help you explore new topics and themes to create truly unique and memorable songs.</li>
        <li><h3 class="sub-section-title">Find inspiration for new songs</h3>Stuck in a creative rut? Lyric Generator can help! Our powerful software generates fresh and exciting lyrics that can inspire you to create your next hit song.</li>
      </ul>
    </section>
  
    <div class="testimonial-container">
      <h2 class="subsection-title">What our users are saying</h2>
      <div class="testimonial">
        <p class="testimonial-text">"Lyric Generator has saved me so much time and energy. As a musician, I love having access to such a powerful tool that helps me create lyrics that truly resonate with my audience."</p>
        <p class="testimonial-author">- John Smith, Singer-Songwriter</p>
      </div>
      <div class="testimonial">
        <p class="testimonial-text">"I'm not the best songwriter, but Lyric Generator has helped me come up with some truly amazing lyrics. I'm so grateful for this software!"</p>
        <p class="testimonial-author">- Sarah Johnson, Amateur Musician</p>
    </div>
    <div class="testimonial">
      <p class="testimonial-text">"I was skeptical at first, but Lyric Generator blew me away with its ability to generate truly original lyrics. I highly recommend this software to anyone looking to improve their songwriting skills."</p>
      <p class="testimonial-author">- David Lee, Music Producer</p>
    </div>
</div>
</main>
<footer>
  <p>Lyric Generator 2023 - Version 0.1.0</p>
</footer>
<style>
  /* styles for the layout */
  main {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 1rem;
    max-width: 800px;
    margin: 0 auto;
  }

  .ad-container {
    display: flex;
    justify-content: space-between;
    margin: 1rem 0;
  }

  .header-container {
    width: 800px;
    margin: 0 auto;
    border-bottom: 1px solid #ccc;
  }

  .header-wrapper {
    text-align: center;
    padding-bottom: 1rem;
    margin-bottom: 2rem;
  }

  .title {
    font-size: 3rem;
    font-weight: bold;
    font-family: Arial, sans-serif;
    margin-top: 1rem;
    margin-bottom: 0.5rem;
  }

  .subtitle {
    font-size: 1.2rem;
    font-family: Arial, sans-serif;
    color: #666;
    margin-bottom: 1rem;
  }

  .main-section {
    margin-bottom: 2rem;
    text-align: center;
  }

  .main-title {
    font-size: 2rem;
    font-weight: bold;
    font-family: Arial, sans-serif;
    margin-bottom: 1rem;
  }

  .subsection-title {
    font-size: 1.5rem;
    font-weight: bold;
    font-family: Arial, sans-serif;
    margin-bottom: 1rem;
  }

  .sub-section-title {
    font-size: 1.2rem;
    font-weight: bold;
    font-family: Arial, sans-serif;
    margin-bottom: 0.5rem;
  }

  .sub-subsection-title {
    font-size: 1.1rem;
    font-weight: bold;
    font-family: Arial, sans-serif;
    margin-bottom: 0.5rem;
  }

  .testimonial-container {
    margin-top: 2rem;
    margin-bottom: 2rem;
    border-top: 1px solid #ccc;
    border-bottom: 1px solid #ccc;
    padding-top: 1rem;
    padding-bottom: 1rem;
  }

  .testimonial {
    margin-top: 1rem;
    margin-bottom: 1rem;
  }

  .testimonial-text {
    font-size: 1.2rem;
    font-family: Arial, sans-serif;
    font-style: italic;
    margin-bottom: 1rem;
  }

  .testimonial-author {
    font-size: 1rem;
    font-family: Arial, sans-serif;
    font-weight: bold;
    text-align: right;
  }
</style>
  