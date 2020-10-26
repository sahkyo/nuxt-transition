<template>
  <section>
    <div class="cover">
      <img src="@/assets/img/paris.jpg" alt="" />
    </div>
    <article class="article__content">
      <nuxt-link to="/" class="back__link">
        ← Retour
      </nuxt-link>
      <h1>Paris</h1>
      <p>
        Son nom ne vous parle probablement pas, et pourtant, Victor Lustig fut
        l’un des plus grands escrocs de son époque. Sa plus grande arnaque ?
        Avoir réussi à se faire passer pour un haut fonctionnaire et vendre à un
        ferrailleur les 7300 tonnes d’acier de la tour Eiffel. À quel prix ?
        Nous ne le saurons jamais… Retour sur l’une des plus grandes
        escroqueries du 20e siècle.
      </p>
      <br />
      <p>
        Né en 1890 dans une famille aisée de la région de Bohème (ancienne
        Autriche-Hongrie), Victor Lustig suit des études plutôt brillantes. Mais
        l’effort et le travail ne l’intéressent pas, et le jeune homme préfère
        mettre à profit son intelligence pour une activité moins fastidieuse, et
        beaucoup plus lucrative : l’escroquerie.
      </p>
      <br />
      <p>
        Victor quitte sa Bohème natale en 1909 et s’installe à Paris. Il débute
        comme proxénète, rencontre les voyous de la capitale, puis embarque pour
        des croisières sur l’Atlantique à bord de bateaux à vapeur et plume aux
        jeux de cartes de riches vieilles dames. Il s’installe quelques années à
        New-York, eldorado du crime organisé, et revient à Paris en 1925. Lui
        vient alors l’idée d’une escroquerie aussi folle que géniale.
      </p>
      <br />
      <p>
        La tour Eiffel, construite pour l’Exposition universelle de 1889, a
        perdu de son éclat. Les visiteurs sont moins nombreux, et les critiques
        toujours aussi vives. Pour compenser son manque d’intérêt touristique,
        Gustave Eiffel tente de bien de la rendre indispensable en réalisant de
        nombreuses expériences scientifiques. Mais en 1925, Eiffel est mort, et
        la Mairie de Paris, propriétaire du monument depuis 1910, ne sait plus
        trop quoi en faire…
      </p>
    </article>
  </section>
</template>

<script>
import gsap from "gsap";
export default {
  transition: {
    enter(el, done) {
      gsap
        .timeline()
        .from(".back__link", {
          autoAlpha: 0,
          yPercent: 100,
          duration: 0.5,
          ease: "power3.inOut"
        })
        .from(".article__content h1", {
          autoAlpha: 0,
          yPercent: 100,
          duration: 0.5,
          ease: "power3.inOut"
        }, "<0.05")
        .from(
          ".article__content p",
          {
            autoAlpha: 0,
            yPercent: 100,
            duration: 0.5,
            ease: "power3.inOut",
            onComplete: done
          },
          "<0.05"
        );
    },
    leave(el, done) {
      gsap.to(el, { autoAlpha: 0, onComplete: done })
    }
  }
};
</script>
