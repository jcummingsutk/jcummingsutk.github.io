---
#date: 2021-04-09T10:58:08-04:00
#description: ""
featured_image: "/images/guay_spellstutter.jpg"
#tags: ["scene"]
title: "A Rebecca Guay Artist Classifier"
---

**Goal**: The purpose for this project is twofold. Immediately, this is a curiosity project, as I wanted to see if I could use techniques I've learned from convolutional neural networks (CNN) not to just identify objects, but also artist styles. Second, it serves as a precursor to one day creating a neural transfer project which takes an input of art and "guayifies" it, turning it into art in the style of Rebecca Guay.

**Results**: A classifier that is 99% accurate in identifying Rebecca Guay's art against other art in Magic: The Gathering.

## Some Useful links
- [this project's github repo](https://github.com/jcummingsutk/art_transformer)
- [The jupyter notebook for this project](https://github.com/jcummingsutk/art_transformer/blob/master/guay_classifier_functional.ipynb)
- [The python mtg sdk](https://github.com/MagicTheGathering/mtg-sdk-python)
- [Scryfall api used to retrieve images](https://scryfall.com/docs/api/cards)
- [A useful paper on artist identification](http://cs231n.stanford.edu/reports/2017/pdfs/406.pdf)
- [Rebecca Guay's Website](http://www.rebeccaguay.com/)


## Discussion
Magic: The Gathering (mtg) is a collectible card game developed by Richard Garfield that can be simply summarized as "Dungeons and Dragons with Cards". One of the great features of it is the great art that comes with it. Personally, I really enjoy art from Rebecca Guay. That's her artwork for Spellstutter Sprite above in the splash.

As mentioned above, this notebook builds a classifier that identifies if a particular piece of art is by Rebecca Guay. I first write a script to find the ids of the artwork by Rebecca Guay, along with the id of other magic cards using the mtg sdk. Once those ids are obtained, I get uris for all of the art done by Guay and not done by Guay using the api from [scryfall](https://scryfall.com/docs/api/cards).

Once obtained, using the functional api of TensorFlow I detach the top of the ResNet50 CNN trained with imagenet weights and freeze those weights. I attach a dense layer and a sigmoid layer to the CNN and use it for classification. Greater than 99% accuracy is obtained on the test set.

The results of this project could more generally be adapted to produce an artist detection application, or an artist selection application where the user takes photos of the art that decorates their walls and can suggest similar artists.
