<template>
  <div>
    <div id="text-clock">
      <!-- line 1 -->
      <p id="line-1">
        <span id="it" class="active">IT</span>L
        <span id="is" class="active">IS</span>AS
        <span id="tgif">GTFI</span>
      </p>
      <!-- line 2 -->
      <p id="line-2">
        AC
        <span id="quarter" class="desc">QUARTER</span>BS
      </p>
      <!-- line 3 -->
      <p>
        <span id="twenty" class="desc">TWENTY</span>
        <span id="five" class="desc">FIVE</span>X
      </p>
      <!-- line 4 -->
      <p>
        <span id="half" class="desc">HALF</span>B
        <span id="ten" class="desc">TEN</span>F
        <span id="to" class="desc">TO</span>
      </p>
      <!-- line 5 -->
      <p>
        <span id="past" class="desc">PAST</span>ERU
        <span id="nine" class="hr">NINE</span>
      </p>
      <!-- line 6 -->
      <p>
        <span id="one" class="hr">ONE</span>
        <span id="six" class="hr">SIX</span>
        <span id="three" class="hr">THREE</span>
      </p>
      <!-- line 7 -->
      <p id="line-7">
        <span id="four" class="hr">FOUR</span>
        <span id="five-hr" class="hr">FIVE</span>
        <span id="two" class="hr">TWO</span>
      </p>
      <!-- line 8 -->
      <p id="line-8">
        <span id="eight" class="hr">EIGHT</span>
        <span id="eleven" class="hr">ELEVEN</span>
      </p>
      <!-- line 9 -->
      <p id="line-9">
        <span id="seven" class="hr">SEVEN</span>
        <span id="twelve" class="hr">TWELVE</span>
      </p>
      <!-- line 10 -->
      <p id="line-10">
        <span id="ten-hr" class="hr">TEN</span>SE
        <span id="oclock" class="desc">OCLOCK</span>
      </p>
      <!-- line 11 -->
      <p id="line-11">
        <span id="midnight" class="hr">MIDNIGHT</span>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  computed: {},
  mounted() {
    var elementsb = document.getElementById('ten')
    console.log(elementsb)
    var self = this
    setInterval(function() {
      self.textClock()
    }, 1000)
    this.textClock()
  },

  methods: {
    textClock() {
      var newDate = new Date(),
        day = newDate.getDay(),
        hours = newDate.getHours(),
        minutes = newDate.getMinutes().toString(),
        seconds = newDate.getSeconds().toString()

      if (hours > 12 && hours !== 0 && hours !== 23) {
        hours = hours - 12
      }
      if (minutes < 10) {
        minutes = 0 + minutes
      }
      if (seconds < 10) {
        seconds = 0 + seconds
      }

      var minsSecs = minutes + seconds
      if (minsSecs > 3230) {
        hours++
      }

      if (day == 5) {
        // var el = document.getElementById('tgif')
        // el.innerHTML = 'TGIF'
        // $('#tgif').html('TGIF')
      }

      var hoursObj = {
        1: '#one',
        2: '#two',
        3: '#three',
        4: '#four',
        5: '#five-hr',
        6: '#six',
        7: '#seven',
        8: '#eight',
        9: '#nine',
        10: '#ten-hr',
        11: '#eleven',
        12: '#twelve',
        23: '#eleven',
        24: '#midnight',
        0: '#midnight'
      }

      this.updateHour(hoursObj[hours])

      if (
        (minsSecs >= 5730 && minsSecs < 6000) ||
        (minsSecs >= 0 && minsSecs < 230)
      ) {
        if (hours !== 24 && hours !== 0) {
          this.updateDesc('oclock')
        }
      } else if (minsSecs >= 230 && minsSecs < 730) {
        this.updateDesc('five, past')
      } else if (minsSecs >= 730 && minsSecs < 1230) {
        this.updateDesc('ten, past')
      } else if (minsSecs >= 1230 && minsSecs < 1730) {
        this.updateDesc('quarter, past')
      } else if (minsSecs >= 1730 && minsSecs < 2230) {
        this.updateDesc('twenty, past')
      } else if (minsSecs >= 2230 && minsSecs < 2730) {
        this.updateDesc('twenty, five, past')
      } else if (minsSecs >= 2730 && minsSecs < 3230) {
        this.updateDesc('half, past')
      } else if (minsSecs >= 3230 && minsSecs < 3730) {
        this.updateDesc('twenty, five, to')
      } else if (minsSecs >= 3730 && minsSecs < 4230) {
        this.updateDesc('twenty, to')
      } else if (minsSecs >= 4230 && minsSecs < 4730) {
        this.updateDesc('quarter, to')
      } else if (minsSecs >= 4730 && minsSecs < 5230) {
        this.updateDesc('ten, to')
      } else if (minsSecs >= 5230 && minsSecs < 5730) {
        this.updateDesc('five, to')
      } else {
        this.updateDesc()
      }
    },
    updateHour(classes) {
      var elementsd = document.querySelectorAll(classes)
      var elementsc = document.querySelectorAll('hr')
      for (var i = 0; i < elementsc.length; i++) {
        console.log('updateHour')
        elementsd[0].classList.add(classes)
        elementsc[0].remove('active')
      }
    },
    updateDesc(classes) {
      var elementsb = document.querySelectorAll(classes)
      var elements = document.querySelectorAll('desc')
      for (var i = 0; i < elements.length; i++) {
        console.log('updateDesc')
        elementsb[0].classList.add(classes)
        elements[0].remove('active')
      }
    }

    //   elementsd.add(classes)
    //   elementsd[0].add('active')
    //   for (var e = 0; e < elementsd.length; e++) {
    //     elementsd[0].add('active')
    //   }
  }
}
</script>

<style>
body {
  background: #000;
  color: #fff;
  font-family: Helvetica, Arial;
  text-align: justify;
  pointer-events: none;
  -webkit-user-select: none;
}

p,
span {
  color: #333333;
  transition: color 0.4s ease-out;
  -ms-transition: color 0.4s ease-out;
  -moz-transition: color 0.4s ease-out;
  -webkit-transition: color 0.4s ease-out;
  letter-spacing: 12.1px;
  font-size: 17px;
}

#midnight {
  color: #000;
  letter-spacing: 23px;
}

#it,
#is,
span.active {
  color: #fff !important;
  transition: color 0.4s ease-out;
  -ms-transition: color 0.4s ease-out;
  -moz-transition: color 0.4s ease-out;
  -webkit-transition: color 0.4s ease-out;
}

#text-clock {
  width: 242px;
  position: absolute;
  left: 50%;
  top: 50%;
  -webkit-transform: translate(-50%, -50%);
  -moz-transform: translate(-50%, -50%);
  -o-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);
  text-transform: uppercase;
}

#line-1,
#line-1 span {
  letter-spacing: 13.9px;
}
#line-2,
#line-2 span {
  letter-spacing: 11.3px;
}
#line-7,
#line-7 span {
  letter-spacing: 11.8px;
}
#line-8,
#line-8 span {
  letter-spacing: 12.3px;
}
#line-9,
#line-9 span {
  letter-spacing: 11.6px;
}
#line-10,
#line-10 span {
  letter-spacing: 11.6px;
}

.hidden {
  display: none;
}
</style>
