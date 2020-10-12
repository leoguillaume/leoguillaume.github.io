---
layout: archive
title: "Posts by topic"
permalink: /posts/
author_profile: true
layouts_gallery:
- url: https://leoguillaume.github.io/ml
  image_path: /assets/images/deep-learning-logo.png
---
<style>

  @import "compass/css3";

  /* Some vars */
  $background-color: hsl(50, 5, 97);
  $black: hsl(200, 40, 10);
  $white: $background-color;
  $base-font-size: 2.4em;
  $base-line-height: 1.5em;

  .ludwig {
  position: relative;
  padding-left: 1em;
  border-left: 0.2em solid lighten($black, 40%);
  font-family: 'Roboto', serif;
  font-size: $base-font-size;
  line-height: $base-line-height;
  font-weight: 100;
  &:before, &:after {
      content: '\201C';
      font-family: 'Sanchez';
      color: lighten($black, 40%);
   }
   &:after {
      content: '\201D';
   }
  }

.column {
  align-content:center;
  float: left;
  width: 50%;
  height: 100%;
}

.column_home {
  align-content:center;
  float: left;
  width: 20%;
  height: 100%;
}


.center_text {
  align-content:center;
  width: 50%;
  vertical-align: middle;
  text-align:justify;
  text-align-last: center;
}

#left-col {
  align-content:center;
  text-align: center;
}

/* Clear floats after the columns */
.row:after {
  content: "";
  display: table;
  clear: both;
}

* {
  box-sizing: border-box;
}

i {
  font-size: 0.4em;
}


#right-col {
  align-content:center;
  text-align: center;
}
</style>
