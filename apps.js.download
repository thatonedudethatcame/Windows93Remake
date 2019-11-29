define({
  'help': {
    cmd: true,
    exec: function() {
      $log('Available commands are : ');
      $log(Object.keys(this._apps).sort().join(', '))
    }
  }
  ,'clear': {
    cmd: true,
    exec: function() {
      $log.clear()
    }
  }
  ,'hist': {
    cmd: true,
    exec: function() {
      $log($cli.history().join('\n'))
    }
  }
  ,'clearhist': {
    cmd: true,
    exec: function() {
      $cli.clearhistory();
      $log('terminal history cleared')
    }
  }
  ,'whois': {
    cmd: true,
    exec: function() {
      $log('Jankenpopp & Zombectro are running the thing, the Mighty Doctor House is hosting the thing.')
    }
  }
  ,'tree': {
    cmd: true,
    exec: function(obj) {
      $log(this._files);
    }
  }
  ,'find': {
    cmd: true,
    exec: function(what, path) {
      if (!what) {
        // http://serverfault.com/questions/124616/how-to-interpret-the-bash-command-usage-syntax
        $log('Usage: find PATTERN [PATH]')
        $log('ex : "find .ttf"');
        $log('ex : "find /\\.ttf$/" (pattern can be a RegEx)');
        $log('ex : "find .ttf c/sys" (optional path)');
        //$log('ex : "find c/files/**.mp3" (or a node glob)');
      }
      var
        f =
        $map($find(what, /*'c/' + */(path || 'c/'), this._files), function(item) {
          //return '<a target="_blank" href="' + encodeURI(item) + '">' + item + '</a>'
          return '<a target="_blank" href="javascript:$exe(\'' + encodeURI(item) + '\')">' + item + '</a>'
        })
        .join('\n')
      ;
      $log.html(f);
    }
  }
  ,'hello': {
    cmd: true,
    exec: function() {
      $log('.__           .__  .__          ');
      $log('|  |__   ____ |  | |  |   ____  ');
      $log('|  |  \\_/ __ \\|  | |  |  /  _ \\ ');
      $log('|   Y  \\  ___/|  |_|  |_(  <_> )');
      $log('|___|  /\\___  >____/____/\\____/ ');
      $log('     \\/     \\/                  ');
      $log('                    .__       .___');
      $log('__  _  _____________|  |    __| _/');
      $log('\\ \\/ \\/ /  _ \\_  __ \\  |   / __ | ');
      $log(' \\     (  <_> )  | \\/  |__/ /_/ | ');
      $log('  \\/\\_/ \\____/|__|  |____/\\____ | ');
      $log('                               \\/');
      $log('Welcome to Windows 93 :)');
      $log('type help or some JavaScript...');
      $log(' ');
    }
  }

  ,'info': {
    cmd: true,
    exec: function() {
      logInfo();
    }
  }

  ,'killall': {
    shortcut: 'ctrl+alt+del', // @todo : shortcut
    exec: function() {
      $io.arr.all(document.querySelectorAll('.ui_window'), function(el) {
        $window.destroy(el);
      });
    }
  }

  ,'terminal': {
    icon: '/c/sys/ico32/terminal.png',
    exec: function(cfg) {
      $terminal(cfg);
    }
  }

  // openers
  /////////////////////////////////////////////////////////////////////////////

  ,'computer': {
    exec: function() {
      $explorer();
    }
  }

  ,'dora': {
    exec: function(path, opt) {
      //console.log(path, opt);
      $explorer(path, opt)
    }
  }

  ,'contact': {
    exec: function(path, opt) {
      var d = "windows93.";
      $alert({
        msg:'<a href="mai'+'lto:contact'+'@'+d+'net">contact'+'@'+d+'net</a>',
        title: 'CONTACT US',
        img: '/c/sys/ico32/mail.png'
      });
    }
  }

  ,'note': {
    exec: function(str, opt) {
      //console.log('hello', arguments);
      if (typeof opt == 'object') {
        if (typeof str == 'string' && !opt.html) opt.html = str;
        $note(opt);
      } else {
        $note(str);
      }
    }
  }

  ,'imageviewer': {
    filetype: ['png','jpg','gif','bmp'],
    exec: function(opt) {
      if (typeof opt == 'string') opt = {url: opt};
      var image = new Image();
      image.src = opt.url;
      image.className = 'ui_layout_center app_imageviewer__img';
      image.onload = load;
      image.onerror = load;
      image.onabort = load;
      function load() {
        if (!opt.height) opt.height = image.height;
        if (!opt.width) opt.width = image.width;
        opt.html = image;
        opt.title = opt.url;
        opt.url = null;
        opt.bodyClass = 'skin_inset_deep ui_layout app_imageviewer' + (opt.bodyClass ? ' ' + opt.bodyClass : '');
        $window(opt);
      }
    }
  }

  ,'layer': {
    exec: function(opt) {
      if (typeof opt == 'string') opt = {url: opt};
      var url = opt.url;
      var image = new Image();
      image.src = url;
      image.onload = load;
      image.onerror = load;
      image.onabort = load;
      function load() {
        opt.url = null;
        $window($extend({
          title: url,
          automaximize: true,
          height: image.height,
          width: image.width,
          baseClass: 'ui_desktop_layer',
          html: image
        }, opt));
      }
    }
  }


  ,'3d': {
    exec: function(txt, color) {

      $window({
        title: txt,
        automaximize: true,
        baseClass: 'ui_desktop_layer',
        url: '/c/programs/apps/3d/index.html?txt=' + txt + '&color=' + color
      });

    }
  }

  ,'opentype': {
    filetype: ['ttf','otf'],
    exec: function(opt) {
      //if (typeof opt == 'string') opt = {url: opt};
      //var url = opt.url;
      console.log(opt.url);
      $window({
        title: 'opentype',
        height: 470,
        width: 757,
        help: '<h1>opentype.js</h1>'
            + '<p><strong>Copyright © 2014 Frederik De Bleser</strong>'
            + '<br><a target="_blank" href=https://raw.githubusercontent.com/nodebox/opentype.js/master/LICENSE">MIT License</p>'
            + '<p><a target="_blank" href="http://nodebox.github.io/opentype.js/">http://nodebox.github.io/opentype.js/</a></p>',
        //baseClass: ,
        url: '/c/programs/apps/opentype/index.php?font=' + opt.url
      });
    }
  }


  // emulators
  /////////////////////////////////////////////////////////////////////////////

    /*
                   !!
               !!!!!!!!!!
           !!!!!!%$""""!!!!!!
       !!$$!!**%%!!!!!!!!%%!!((t
   !!!!. #### !!!**++++%%**((""M
  " ...!.t''t.!!!!!!!**((""%%%%M
  "`!!!....!!'!!'uu((""%%%%""##t
  " !!!!!!!..!(((""%%%%""##tt
   !!((!!!!!!!"%%%%""##tt
       !!((!!!(""##tt
           !!!ttt
    */

  ,'dmg': {
    filetype: ['gb','gbc'],
    exec: function(opt) {

      var about =
        '<h1>JavaScript GameBoy Color Emulator</h1>'
      + '<p><strong>Copyright (C) 2010 - 2012 <a target="_blank" href="https://github.com/grantgalitz">Grant Galitz</a></strong></p>'
      + '<p><a target="_blank" href="https://github.com/grantgalitz/GameBoy-Online">https://github.com/grantgalitz/GameBoy-Online</a></p>'
      + '<p>A GameBoy Color emulator that utilizes HTML5 canvas and JavaScript audio APIs to provide a full emulation of the console.</p>'
      + '<p>This program is free software; you can redistribute it and/or modify it under the terms of the GNU General Public License version 2 as published by the Free Software Foundation.<br>'
      + 'The full license is available at <a target="_blank" href="http://www.gnu.org/licenses/gpl.html">http://www.gnu.org/licenses/gpl.html</a><br>'
      + 'This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.</p>'
      + '<p>Keyboard Controls:\nX/J/[numpad enter] are A.\nZ/Y/Q/[numpad 3] are B.\nShift/[numpad 0] is Select.\nSpace/[numpad .] is Start.\nThe d-pad is the control pad.</p>'
      ;

      opt = opt || {};
      opt.url = '/c/programs/emulators/dmg/play.php' + (opt.url ? '?rom='+opt.url : '');
      opt.help = about;
      opt.minWidth = true;
      opt.minHeight = true;
      opt.width = '160';
      opt.height = '144';
      opt.bodyClass = 'skin_inset_deep';
      $window(opt);
    }
  }
/*
  ,'sms': {
    filetype: ['sms'],
    exec: function(opt) {

      var about =
        '<h1>Miracle</h1>'
      + '<b>a Sega Master System emulator in Javascript</b>'
      + '<p>By <a target="_blank" href="http://xania.org/">Matt Godbolt</a></p>'
      + '<p>Based on <a target="_blank" href="http://matt.west.co.tt/category/javascript/jsspeccy/">JSSpeccy</a> by <a target="_blank" href="http://matt.west.co.tt/">Matt Westcott</a></p>'
      + '<p>..which in turn is based on <a target="_blank" href="http://fuse-emulator.sourceforge.net/">Fuse</a> by Philip Kendall et al. Icons from <a target="_blank" href="http://www.icon-king.com/projects/nuvola/">Nuvola</a> by David Vignoni.</p>'
      + '<p>This program is <a target="_blank" href="http://github.com/mattgodbolt/Miracle">free software</a>: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.</p>'
      + '<p>This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more details.</p>'
      + '<p>You should have received a copy of the GNU General Public License along with this program.  If not, see &lt;<a target="_blank" href="http://www.gnu.org/licenses/">http://www.gnu.org/licenses/</a>&gt;.</p>'
      + '</div>'
      ;

      opt = opt || {};
      opt.url = '/c/programs/emulators/sms/play.php' + (opt.url ? '?rom='+opt.url : '');
      opt.help = about;
      opt.minWidth = true;
      opt.minHeight = true;
      opt.width = '256';
      opt.height = '192';
      opt.bodyClass = 'skin_inset_deep';
      $window(opt);
    }
  }

  ,'atarist': {
    filetype: ['st', 'sts', 'msa'],
    exec: function(opt) {

      var about =
        '<h1>Miracle</h1>'
      + '<b>a Sega Master System emulator in Javascript</b>'
      + '<p>By <a target="_blank" href="http://xania.org/">Matt Godbolt</a></p>'
      + '<p>Based on <a target="_blank" href="http://matt.west.co.tt/category/javascript/jsspeccy/">JSSpeccy</a> by <a target="_blank" href="http://matt.west.co.tt/">Matt Westcott</a></p>'
      + '<p>..which in turn is based on <a target="_blank" href="http://fuse-emulator.sourceforge.net/">Fuse</a> by Philip Kendall et al. Icons from <a target="_blank" href="http://www.icon-king.com/projects/nuvola/">Nuvola</a> by David Vignoni.</p>'
      + '<p>This program is <a target="_blank" href="http://github.com/mattgodbolt/Miracle">free software</a>: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.</p>'
      + '<p>This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more details.</p>'
      + '<p>You should have received a copy of the GNU General Public License along with this program.  If not, see &lt;<a target="_blank" href="http://www.gnu.org/licenses/">http://www.gnu.org/licenses/</a>&gt;.</p>'
      + '</div>'
      ;

      opt = opt || {};
      opt.url = '/c/programs/emulators/atarist/play.php' + (opt.url ? '?rom='+opt.url : '');
      opt.help = about;
      opt.minWidth = true;
      opt.minHeight = true;
      opt.width = '320';
      opt.height = '200';
      opt.bodyClass = 'skin_inset_deep';
      $window(opt);
    }
  }

  ,'zx': {
    filetype: ['tap', 'tzx', 'sna', 'z80'],
    exec: function(opt) {

      var about =
        '<h1>JSSpeccy</h1>'
      + '<b>a ZX Spectrum emulator in Javascript</b>'
      + '<p>By <a target="_blank" href="http://matt.west.co.tt/">Matt Westcott</a></p>'
      + '<p>Sound routines by Darren Coles</p>'
      + '<p><a target="_blank" href="http://matt.west.co.tt/category/javascript/jsspeccy/">JSSpeccy homepage</a> (including downloads and source code)</p>'
      + '<p>Based on <a target="_blank" href="http://fuse-emulator.sourceforge.net/">Fuse</a> by Philip Kendall et al. Icons from <a target="_blank" href="http://www.icon-king.com/projects/nuvola/">Nuvola</a> by David Vignoni.</p>'
      + '<p>This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.</p>'
      + '<p>This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more details.</p>'
      + '<p>You should have received a copy of the GNU General Public License along with this program.  If not, see &lt;<a target="_blank" href="http://www.gnu.org/licenses/">http://www.gnu.org/licenses/</a>&gt;.</p>'
      + '</div>'
      ;

      opt = opt || {};
      opt.url = '/c/programs/emulators/zx/play.php' + (opt.url ? '?rom='+opt.url : '');
      opt.help = about;
      opt.width = '320';
      opt.height = '240';
      opt.bodyClass = 'skin_inset_deep';
      $window(opt);
    }
  }*/


  ,'bytebeat': {
    exec: function(opt) {
      opt = {};//$extend({}, opt);
      opt.title = 'ByteBeat';
      opt.help = "<b>Credits :</b><br><a target=_blank href='https://github.com/greggman/html5bytebeat'>https://github.com/greggman/html5bytebeat</a>";

      opt.icon = '/c/sys/ico32/bytebeat.png';
      //opt.url = '/c/programs/apps/bytebeat/index.php#t=0&e=1&bb=5d000001006100000000000000003a08022391d5293f69c2e49ecf68456c28c2632528daade8252cb47f5549995f49189b4bbd1728c98726b7aa31fd79883bd31e5b84a9d1ec5dfea5819b1622e4be7fffef360000';
      opt.url = '/c/programs/apps/bytebeat/index.php';
      opt.width = '700';
      opt.height = '400';
      opt.bodyClass = 'skin_inset_deep';
      $window(opt);
    }
  }

  ,'edit': {
    filetype: [/*'html','htm','php',*/'txt','md','nfo','diz','css','js','json'],
    exec: function(file, cb, update) {

      if (typeof file == 'string') file = {url: file};
      if (!file) file = {url: ''};

      $loader([
         '/c/libs/codemirror/lib/codemirror.js'
        ,'/c/libs/codemirror/keymap/sublime.js'
        ,'/c/libs/codemirror/mode/css/css.js'
        ,'/c/libs/codemirror/mode/javascript/javascript.js'
        //,'/c/libs/codemirror/mode/markdown/markdown.js'
        ,'/c/libs/codemirror/mode/xml/xml.js'
        ,'/c/libs/codemirror/lib/codemirror.css'
        ,'/c/libs/codemirror/theme/cobalt.css'
      ], function(CodeMirror) {
        //console.log('CodeMirror is a function', typeof CodeMirror === 'function');
        //console.log('javascript mode is defined', CodeMirror.defaults.mode === 'javascript');
        //console.log('css mode is defined', CodeMirror.defaults.mode === 'css');

        function openFile(file) {
          if (file.indexOf('a/')===0) {
            //console.log('local', file.replace(/^a\//,''));
            $db.get(file.replace(/^a\//,''), function(err, val) {
              //console.log(val);
              readFile('text/plain', val);
            });
          } else {
            $ajax.get(file)
              .done(function(data, status, xhr, isJson) {
                var ct = xhr.getResponseHeader("content-type") || "";
                var mime = isJson ? 'application/json' : ct.split(';').shift();
                var ext = $url.getExtention(file);
                if (ext == 'xml' || ext == 'rss') mime = 'xml';
                readFile(mime, xhr.responseText);
              })
              .fail(function() {
                $error('Can\'t load file');
              })
            ;
          }
        }

        function readFile(mime, text) {
          editor.setOption("mode", mime);
          editor.setValue(text);
          setTimeout(function() {
            editor.refresh();
          },10);
          if (typeof update == 'function') update(text);
        }

        var
          editor,
          action = {
            new: function() {editor.setValue('')},
            open: function() {
              $explorer('c/', {browse:true, list:true, onclose: function(ok, file) {
                //console.log(arguments);
                if (ok) openFile(file)
              }})
            },
            about: function() {
              $alert({
                title: 'About',
                //width: 450,
                msg: '<b>CodeMirror</b> is a versatile text editor implemented in JavaScript for the browser.<br><b>Copyright (C) 2014 by Marijn Haverbeke</b><br>MIT license<br><a href="http://codemirror.net" target="_blank">codemirror.net</a>',
                img: '/c/libs/codemirror/doc/logo.png',
                onopen: $noop
              });
              //$info('<img src="/c/libs/codemirror/doc/logo.png">CodeMirror is a versatile text editor implemented in JavaScript for the browser.<br><a href="http://codemirror.net" target="_blank">codemirror.net</a>')
            }
          },
          menu = [
            {name: 'File', items: [
              {name: 'New', action: action.new},
              {name: 'Open', action: action.open}]},
            {name: 'About', action: action.about}
          ],
          create = function(body) {

            editor = CodeMirror(body, {
               theme: 'default' //'cobalt'
              ,mode: 'text/x-markdown' //'text/javascript'  //'application/json'
              ,lineWrapping: true
              ,lineNumbers: true
              ,indentUnit: 2
              //,keyMap: 'sublime'
              //,value: 'txt'
            });

            openFile(file.url);
            editor.refresh();
            return editor;
          }
        ;

        if (typeof cb == 'function') {
          cb(create);
        } else {
          $window({
            title: 'CodeMirror',
            menu: menu,
            bodyClass: 'ui_texteditor skin_inset_deep',
            width: 435,
            height: 345,
            onresize: function() {
              //console.log('resize')
              editor.refresh();
            },
            onopen: function(_, body) {
              create(body);
            }
          });
        }

      });

    }
  }

  // apps
  /////////////////////////////////////////////////////////////////////////////

  ,'catex': {
    exec: function(theurl) { 'use strict';
      var scope = this;
      $loader([
         '/c/programs/apps/catExplorer/catExplorer.js' // <-------- catExplorer's mess moved to it's own file ;)
      ], function(catex) {
        catex.exec(scope, theurl);
      });
    }
  }

  ,"pony": {
    exec: function() {
      var scope = this;

      var anim = {
        'Invert': $loop(function() {
            scope._everything.classList.toggle('invert');
          })
        ,'Tada': $loop(function() {
            scope._everything.classList.toggle('tada');
            scope._everything.classList.toggle('animate');
          },100)
        ,'Hue': $loop(function() {
            scope._everything.style.filter = 'hue-rotate('+Math.random()*360+'deg)';
            scope._everything.style.webkitFilter = 'hue-rotate('+Math.random()*360+'deg)';
          })
        ,'Blur': $loop(function() {
            scope._everything.style.filter = 'blur('+Math.random()*60+'px)';
            scope._everything.style.webkitFilter = 'blur('+Math.random()*60+'px)';
          })
        ,'Saturate': $loop(function() {
            scope._everything.style.filter = 'saturate('+Math.random()*500+'%)';
            scope._everything.style.webkitFilter = 'saturate('+Math.random()*500+'%)';
          })
        ,'Contrast': $loop(function() {
            scope._everything.style.filter = 'contrast('+Math.random()*1500+'%)';
            scope._everything.style.webkitFilter = 'contrast('+Math.random()*1500+'%)';
          })
      }

      var layout = {
        'default' : [
          "f1 f2 f3 f4 f5 f6 f7 f8 f9 f10 f11 f12",
          "1 2 3 4 5 6 7 8 9 0 backspace",
          "tab a z e r t y u i o p ^ $",
          "caps q s d f g h j k l m \u00f9 * enter",
          "shift < w x c v b n , ; : !",
          "ctrl alt space"
        ]
      }

      var poney = {};
      var poneyFn = {};
      var poneyFill = {};

      var layoutDiv = document.createElement('div');
      layoutDiv.className = 'vj_layout'
      var lineDiv = document.createElement('div');
      var keyDiv = document.createElement('button');
      function displayLayout(layout) {
        $io.arr.all(layout, function(line) {
          var lineD = lineDiv.cloneNode(false);
          layoutDiv.appendChild(lineD);
          var keys = line.split(' ');
          $io.arr.all(keys, function(k) {
            var kk = keyDiv.cloneNode(false);
            //console.log(kk);
            kk.innerHTML = k;
            kk.id = 'vj_key_' + k;
            lineD.appendChild(kk);
            kk.addEventListener('focus', function() {
              current.textContent = k;
              //if (vj_sound[k]) sound.value = vj_sound[k];
              $io.obj.all(poney, function(item, key) {

                //console.log('key', item, key);
                poneyFill[key](item[k] || '');
              });
            }, false);
          })
        });
        return layoutDiv;
      }

      var ui = document.createElement('div');
      ui.appendChild(displayLayout(layout['default'])); //'yo';

      var keys = {};

      var
         vjCombo = document.createElement('div')
        ,truc = document.createElement('div')
        ,image = document.createElement('input')
        ,klass = document.createElement('input')
        ,js = document.createElement('textarea')
      ;
      vjCombo.className = 'vj_truc';


      //var selectEffects = document.getElementById('select_effects');

      function createSelector(what, fn) {
        //poney[what];
        poney['sound'] = $dbls({}, 'vj/sound', function() {
          return poney['sound']
        });
        poney['effect'] = $dbls({}, 'vj/effect', function() {
          return poney['effect']
        });
        /*$db({}, 'vj/'+what,
          function(val) {
            poney[what] = val;
          },
          function() {return poney[what]}
        );*/
        var labelsound = document.createElement('label');
        var labeleffect = document.createElement('label');
        var inp = document.createElement('input');
        //var effect = selectEffects.cloneNode(true);//document.createElement('select');
        //effect.id = '';
        var btn = document.createElement('button');
        var div = vjCombo.cloneNode(false);
        inp.placeholder = 'sound';
        inp.className = 'vj_input' + what;
        div.appendChild(inp);
        div.appendChild(btn);
        btn.innerHTML = 'Import';
        labelsound.textContent = 'Choose a sound';
        labeleffect.textContent = 'Choose an effect';
        //truc.appendChild(labelsound);
        truc.appendChild(div);

        var effect = $el.create('select', null,
          {class: 'vj_select_effects'},
          [
            $el.create('option', '--- effects ---', {value: ''}),
            $el.create('option', 'none', {value: ''}),
            $el.create('option', 'acid', {value: 'ef_acid'}),
            $el.create('option', 'blur', {value: 'ef_blur'}),
            $el.create('option', 'invert', {value: 'ef_invert'}),
            $el.create('option', 'edge', {value: 'ef_edge'}),
            $el.create('option', 'zombi', {value: 'ef_zombi'}),
            $el.create('option', 'emboss', {value: 'ef_emboss'}),
            $el.create('option', 'xray', {value: 'ef_xray'}),
            $el.create('option', 'turbulence', {value: 'ef_turbulence'}),
            $el.create('option', 'glitch', {value: 'ef_glitch'}),
            $el.create('option', 'spectrum', {value: 'ef_spectrum'}),
            $el.create('option', 'Volvo', {value: 'volvo'}),
            $el.create('option', 'Saab', {value: 'saab'}),
            $el.create('option', 'Mercedes', {value: 'mercedes'}),
            $el.create('option', 'Audi', {value: 'audi'})
          ],
          truc
        );
        effect.style.display = 'none';
        //truc.appendChild(labeleffect);
        //truc.appendChild(effect);
        /*btn.addEventListener('click', function() {
          $explorer('/c/sounds', {explorer:true, browse:true, onclose:function(ok, val) {
            inp.value = val;
            poney['sound'][current.textContent] = val;
            poneyWindow.focus();
          }});
        }, false);*/
        btn.onclick = function() {
          $explorer('/c/files/sounds/', {list:true, browse:true, onclose:function(ok, val) {
            inp.value = val;
            poney['sound'][current.textContent] = val;
            poneyWindow.focus();
          }});
        };
        effect.onchange = function() {
          poney['effect'][current.textContent] = this.value;
        };
        poneyFn['sound'] = function(val) {
          //fn(val);
          $sound(val).play();
        };
        poneyFn;['sound'].stop = function(val) {
          //fn(val);
          $sound(val).stop();
        };
        poneyFn['effect'] = function(val) {
          scope._everything.classList.add(val);
        };
        poneyFn['effect'].stop = function(val) {
          scope._everything.classList.remove(val);
        };
        poneyFill['sound'] = function(val) {
          inp.value = val;
        };
        poneyFill['effect'] = function(val) {
          var ef = effect.querySelectorAll('option');
          $io.arr.all(ef, function(item) {
            //console.log(item.value, val)
            if (item.value == val) item.selected = true;
          });
        };
      }

      createSelector();
    /*  createSelector('sound', function(item) {
        $sound(item).play();

      });*/

      var current = document.createElement('div');
      current.className = 'vj_current';
      ui.appendChild(current);
      ui.appendChild(truc); //'yo';


      function popitup(url) {
        var newwindow = window.open(url,'vjmonitor','location=0,toolbar=0,menubar=0,directories=0,status=0,height=300,width=500');
        if (window.focus) {newwindow.focus()}
        return false;
      }

      var preview;
      function vj(fn) {
        fn(preview);
      }
      vj.listen = function(fn) {
        preview = fn();
        if (!preview) return;
        preview.style.background = 'red';
      }
      vj.popup = function() {
        popitup('/vjpreview.html');
      }

      var poneyWindow = null;

      vj.open = function() {
        current.textContent = 'Click on a key, assign effects, then press that key on your keyboard... PONEY PARTY \\m/'

        $window({
          title:'poney jockey',
          icon:'c/sys/ico32/poney.gif',
          bodyClass: 'ui_vj skin_base',
          html: ui,
          animationIn: false,
          width: 500,
          height: 250,
          onopen: function(el) {

            /*setTimeout(function() {
              $error('EPILEPSY WARNING<br>Microsoft VBScript runtime (0x800A01AD)<br> ActiveX component can\'t create object:<br> PONEY JOCKEY (beta unstable version) is opening the gates of hell!');
            }, 100);*/

            poneyWindow = el;
            $key.down(document.body, function(k) {
              var keyEleme = document.getElementById('vj_key_' + k);
              if (keyEleme && !keyEleme.classList.contains('pressed')) {
                keyEleme.classList.add('pressed');
                keys[k] = true;
                $io.obj.all(poney, function(item, key) {
                  if (item[k]) poneyFn[key](item[k]);
                });
              };
              return false;
            });
            $key.up(document.body, function(k) {
              var keyEleme = document.getElementById('vj_key_' + k);
              if (keyEleme && keyEleme.classList.contains('pressed')) {
                keyEleme.classList.remove('pressed');
                keys[k] = false;
                $io.obj.all(poney, function(item, key) {
                  if (item[k] && poneyFn[key] && poneyFn[key].stop) poneyFn[key].stop(item[k]);
                });
              };
              return false;
            });
            $key(document.body, function() {
              return false;
            });
          }/*,
          onclose: function(el) {
            $key(function(k) {
              console.log(k);
            });
          }*/
        });
      }

      vj.open();

    }
  }

  ,"manifesto": {
    exec: function() {

      /////////////////////////////////////////////////////////////////////////////
      // Samy is my hero
      /////////////////////////////////////////////////////////////////////////////
      // life ruined my internet
      /////////////////////////////////////////////////////////////////////////////

      var A = [
        'retro-engineering',
        'reverse engineering',
        'deprogrammed obsolescence',
        'media archeology',
        'recycling',
        'retrocomputing',
        'parody',
        'inception',
        '666',
        'acid',
        'freedom',
        'infinity',
        'pony',
        'art',
        'demoscene',
        'memetic',
        'hysteria',
        'proselytism',
        'thought contagion',
        'dolphin',
        'corgi',
        'doge',
        'hydra',
        'helix',
        'yoda',
        'cat',
        'glitch',
        'troll',
        'noob',
        'ninja',
        'wizard',
        //'lisa',
        'lenna'
      ], B = [
        'easter egg',
        'php',
        'html',
        'html5',
        'javascript',
        //'localStorage',
        'web3.0',
        'NaN',
        'Infinity',
        'random',
        'Math.random()',
        'π',
        'inception',
        'css3',
        'css',
        'free software',
        'prosthetic knowledge',
        '(x,y,z)',
        'virus',
        'internet',
        'wifi',
        'open source',
        'GNU',
        'OS',
        'linux',
        'unix',
        'hyperlink',
        //'copyleft',
        'creative commons',
        'MySQL',
        'RSS',
        'nodejs',
        'server',
        'hack',
        'iframe',
        'canvas',
        'glitch',
        'ASCII',
        'utf-8',
        'emoji',
        'cthulhu',
        'unicode'
      ], C = [
        'uchronia',
        'popart',
        'anachronism',
        'dadaism',
        'surrealism',
        'new-realism',
        'meta-realism',
        'future',
        'matrix',
        'inception',
        'unproductivity',
        'procrastination',
        'useless',
        'unprofitability',
        'spaghetti code',
        'viral',
        'acid',
        'epic fail',
        'epic win',
        'fap',
        'swag',
        'Z̤̲̙̙͎̥̝A͎̣͔̙͘L̥̻̗̳̻̳̳͢G͉̖̯͓̞̩̦O̹̹̺',
        'nope',
        'chuck norris',
        'over 9000',
        'meta',
        'meta-meta',
        'lulz',
        'poop',
        'glitch',
        'life',
        'system32.dll',
        'myspace',
        'loominati',
        'poney',
        'cthulhu',
        'zerg rush',
        'forever alone',
        'hug',
        'manifesto',
        'internet for ever',
        'fuck the cloud',
        'web3.0',
        'fixing the internet'
      ];

      var WTF = [A,B,C];

      function chance(p) { return (Math.random() * 100 >= (p || 50)) ? false : true }

      /*function getMethods(obj) {
        var result = [];
        for (var id in obj) {
          try {
            if (typeof(obj[id]) == "function") {
              result.push(id);
            }
          } catch (err) {
            result.push(id);
          }
        }
        return result;
      }*/

      function idea() {
        if (chance(2)) {
          //console.log('R*3');
          var str = $io.arr.random($io.arr.random(WTF));
          return str + ' + ' + str + ' = ' + str
        }
        if (chance(10)) {
          //console.log('R,R,R');
          return $io.arr.random($io.arr.random(WTF))+ ' + ' + $io.arr.random($io.arr.random(WTF)) + ' = ' + $io.arr.random($io.arr.random(WTF))
        } else {
          //console.log('A,B,C');
          return $io.arr.random(A) + ' + ' + $io.arr.random(B) + ' = ' + $io.arr.random(C)
        }
      }

      //var QUACK;
      function m() {
        var msg = idea();
        $error({
           msg: msg
          ,title: 'MANIFESTO'
          ,img: '/c/sys/ico32/question.png'
          ,btnCancel: 'wtf?'
          ,animationIn: ''
          ,animationOut: ''
          ,oncancel: function(ok) {
            //if (!QUACK) QUACK = $sound('/c/sys/sounds/QUACK.ogg');
            //QUACK.play();
            $sound('/c/sys/sounds/QUACK.ogg').play();
            this.el.body.querySelector('.ui_alert__text').innerHTML = idea();
            return false;
          }
        });
      }
      m();

    }
  }

  // games
  /////////////////////////////////////////////////////////////////////////////

  ,"solitude": {
    exec: function() {
      var iframe;
      var data = {
        url: '/c/programs/games/solitude/index.html',
        icon: '/c/sys/ico32/solitaire.gif',
        title: 'Solitude',
        width: 630,
        height: 440,
        onopen: function(el) {
          iframe = this.el.iframe; //el.getElementsByTagName('iframe')[0];
        },
        menu: [{name: 'Game', items: [
          {name: 'New', action: function() {
            iframe.contentWindow.newGame();
          }},
          {name: 'Retry', action: function() {
            iframe.contentWindow.klondike();
          }},
          {name: 'Yeah', action: function() {
            $alert('click and drag anywhere on the game to see the fun, thanks to mr doob');
            iframe.contentWindow.mrdoob();
          }}
        ]}]
      };
      $window(data);
    }
  }

  ,"potato": {
    exec: function() {
      var data = {
         url: 'https://www.youtube.com/embed/C7fKoamz0nY?showinfo=0&amp;autoplay=1'
        ,icon: '/c/sys/ico32/potato.png'
        ,title: 'POTATO'
        ,width: 560
        ,height: 315
      };
      $window(data);
    }
  }
  ,"anthology": {
    exec: function() {
      var data = {
         url: 'https://www.youtube.com/embed/sy8Utr0CvBI?showinfo=0&amp;autoplay=1'
        ,icon: '/c/sys/ico32/trophy.gif'
        ,title: 'ANTHOLOGY'
        ,width: 560
        ,height: 315
      };
      $window(data);
    }
  }



  ,"live": {
    exec: function() {
      var data = {
         url: 'https://www.youtube.com/embed/x9xDXU2WJeY?showinfo=0&amp;autoplay=1'
        ,icon: '/c/sys/ico32/sound_on.png'
        ,title: 'Windows93™ LIVE BAND'
        ,width: 560
        ,height: 315
      };
      $window(data);
    }
  }




  ,"castlegafa": {
    exec: function() {
      var data = {
         url: '/c/programs/games/castleGafa/index.html'
        ,icon: '/c/programs/games/castleGafa/icon.gif'
        ,title: 'Castle GAFA 3D'
        ,help: '<b>Credits :</b><br><a target="_blank" href="https://github.com/loadx/html5-wolfenstein3D">https://github.com/loadx/html5-wolfenstein3D</a><br><a target="_blank" href="http://3d.wolfenstein.com">http://3d.wolfenstein.com</a>'
        ,width: 640
        ,height: 400
      };
      $window(data);
    }
  }
  ,"defrag": {
    exec: function() {
      var data = {
         url: '/c/programs/games/defrag/index.php'
        ,title: 'DEFRAG'
        ,width: 640
        ,height: 495
      };
      $window(data);
    }
  }
  ,"glitchgirlz": {
    exec: function() {
      $exe('dmg', {url: '/c/files/roms/dmg/fail/Glitch_Grrrlz-Vol01.gbc'})
    }
  }

  // easter eggs / jokes / virus
  /////////////////////////////////////////////////////////////////////////////

  /*,'global thermonuclear war': {
    exec: function(what, path) {
      var
         line1 = $log('|   |   |   |')
        ,lineN = $log('-------------')
        ,line2 = $log('|   |   |   |')
        ,lineN = $log('-------------')
        ,line3 = $log('|   |   |   |')
      ;
    }
  }*/

  ,"fx": {
    cmd: true,
    exec: function(name) {
      var scope = this;

      var oldTransform;
      function repaint(cl) {
        oldTransform = scope._everything.style.webkitTransform;
        scope._everything.style.webkitTransform = 'scale(1)';
        scope._everything.classList.toggle(cl);
        scope._everything.style.webkitTransform = oldTransform;
      }

      var effects = {
         'blur':         function() { repaint('ef_blur')  }
        ,'acid':         function() { repaint('ef_acid')  }
        ,'invert':       function() { repaint('ef_invert')  }
        ,'invertLight':  function() { repaint('ef_invert_light')  }
        ,'grayscale':    function() { repaint('ef_grayscale')  }
        ,'xray':         function() { repaint('ef_xray')  }
        ,'zombi':        function() { repaint('ef_zombi')  }
        ,'emboss':       function() { repaint('ef_emboss')  }
        ,'edge':         function() { repaint('ef_edge')  }
        ,'convo':        function() { repaint('ef_convo')  }
        ,'spectrum':     function() { repaint('ef_spectrum')  }
        ,'noir':         function() { repaint('ef_noir')  }
        ,'hip':          function() { repaint('ef_hip')  }
        ,'blueray':      function() { repaint('ef_blueray')  }
      }

      if (!name) {
        $log('Available effects :');
        $log(Object.keys(effects).sort().join(', '));
        return;
      };

      if (effects[name]) effects[name]();
      else $log.error('The effect ' + name + ' does not exist.');
    }
  }

  ,"acid": {
    exec: function() {
      // alias
      $exe('fx acid');
    }
  }

  ,"rotate": {
    exec: function() {
      if(this._everything.classList.contains('rotate')) {
        this._everything.classList.remove('rotate');
        this._everything.classList.add('unrotate');
      } else {
        this._everything.classList.remove('unrotate');
        this._everything.classList.add('rotate');
      }
    }
  }

  ,"gravity": {
    exec: function() {
      this.load([
        '/c/libs/jquery.min.js',
        '/c/libs/jGravity-min.js'
      ], function() {
        $('#w93_desktop').jGravity({target:'.ui_icon,.ui_window', depth:15})
      });
    }
  }

  ,"lisa": {
    exec: function() {
      $exe('layer', {
        title: 'lisa',
        url: '/c/files/images/gif/lisa.gif',
        onopen: function(win) {
          setTimeout(function() {
            win.style.top = 'auto';
            win.style.left = 'auto';
            win.style.right = '-140px';
            win.style.bottom = '-20px';
          }, 100);
        },
        automaximize:false
      });
    }
  }

  ,"hydra": {
    exec: function() {
      function hydra() {
        $alert({
          msg:'Cut off a head, two more will take its place.<br>[ Hydra ViRuS BioCoded by Typhon/Échidna ]',
          title: 'HYDRA',
          img: '/c/sys/ico32/hydra.png',
          baseClass: 'virus virus--hydra ui_alert',
          center: false,
          cb: function(ok) {
            hydra();
            hydra();
          }
        });
      }
      hydra();
    }
  }

  ,"doctor": {
    exec: function(arg, term) {
      var scope = this;
      function killAllVirus(succes, fail) {

        scope._everything.classList.remove('acid');
        scope._everything.classList.remove('rotate');
        scope._everything.classList.remove('invert');
        scope._everything.classList.remove('grayscale');
        scope._everything.setAttribute('style', '');

        // check if any cmd have a doctor function...
        if (!scope._data.doctor) scope._data.doctor = {};
        else {
          var vaccin = scope._data.doctor;
          for (var key in vaccin) {
            if (vaccin.hasOwnProperty(key)) {
              vaccin[key]();
            }
          }
        }
        var virus = document.querySelectorAll('.virus');
        if (virus.length) {
          $io.arr.all(virus, function(el) {
            $window.destroy(el);
          });
          if (succes !== false) $docAlert(succes || "All Virus Killed !");
        } else {
          if (fail !== false) $docAlert(fail || "No Virus detected.");
        };
      }
      function $docAlert(msg) {
        $alert({
          title: 'Doctor Marburg Antivirus',
          img: '/c/sys/ico32/doctor.gif',
          btnOk: 'Thanks !',
          msg: msg
        });
      }


      var funnyDoctorMarburg = [

        function() {
          $confirm({
            title:'Doctor Marburg Antivirus',
            img:'/c/sys/ico32/doctor.gif',
            btnOk: 'Yep!',
            btnCancel: 'Nope!',
            msg:"That Hydra virus again ?"
          }, function(isOk) {
            isOk && killAllVirus("Don't click on it next time", "Are you kidding? There is no Hydra here!");
          })
        }
        ,
        function() {
          $confirm({
            title:'Doctor Marburg Antivirus',
            img:'/c/sys/ico32/doctor.gif',
            btnOk: 'Breathe',
            msg:"Breathe in and out please..."
          }, function(isOk) {
            isOk && killAllVirus('Inhale inhale. You\'re the victim', 'Diagnostic : Psycho-somatic addict-insane');
          })
        }
        ,
        function() {
          $prompt({
            title:'Doctor Marburg Antivirus',
            img:'/c/sys/ico32/doctor.gif',
            btnOk: 'Say it',
            msg: 'Say 99...'
          }, function(isOk, res) {
            if (isOk && res == '99') {
              killAllVirus();
            } else if (isOk) {
              $confirm({
                title:'Doctor Marburg Antivirus',
                img:'/c/sys/ico32/doctor.gif',
                btnOk: "Let's do that",
                msg:"Mhh, you're very sick, unfortunately I can't do anything for you... Except cleaning your computer"
              }, function(isOk, res) {
                if (isOk) {
                  killAllVirus();
                }
              });
            }
          })
        }
        ,
        function() {
          $confirm({
            title:'Doctor Marburg Antivirus',
            img:'/c/sys/ico32/doctor.gif',
            msg:'Welcome to Doctor Marburg Antivirus.<br>Would you like to clean your System ?'
          }, function(isOk, res) {
            if (isOk) {
              $confirm({
                title:'Doctor Marburg Antivirus',
                img:'/c/sys/ico32/doctor.gif',
                btnOk: 'Sure',
                btnCancel: 'Not Really',
                msg:'<b>Warning !</b><br>Doctor Marburg is not responsible for direct, indirect, incidental or consequential damages resulting from any defect, error or failure to perform this ilegal operation.<br><br>Do you want to perform anyway ?'
              }, function(isOk, res) {
                if (isOk) {
                  $prompt({
                    title:'Doctor Marburg Antivirus',
                    img:'/c/sys/ico32/doctor.gif',
                    btnCancel: 'Never Mind',
                    msg: 'Ok, please confirm with your credit card number'
                  }, function(isOk, res) {
                    if (isOk) {
                      $docAlert("<b> Ilegal operation detected !</b><br>DOCTOR MARBURG had blocked the following malware application to perform an ilegal operation : <br><br><i>DOCTOR MARBURG - ilegal Operation detected</i>");
                    } else {
                      $confirm({
                        title:'Doctor Marburg Antivirus',
                        img:'/c/sys/ico32/doctor.gif',
                        btnOk: 'Sure',
                        msg:'I was just testing you ;)<br>Do the cleaning operation anyway ?'
                      }, function(isOk, res) {
                        if (isOk) {
                          killAllVirus();
                        }
                      });
                    }
                  });
                } else {
                  $docAlert("You're such a Pussy :p");
                }
              });
            } else {
              killAllVirus("Well, I did it anyway ^^", false);
            }
          })
        }
      ];

      if (document.querySelector('.virus--hydra')) {
        funnyDoctorMarburg[0]();
      } else {
        $io.arr.random(funnyDoctorMarburg)();
      }

    }
  }

  // jquery
  /////////////////////////////////////////////////////////////////////////////

  ,"glitch": {

    exec: function(arg, term) {
      var scope = this;
      this.load([
        '/c/libs/html2canvas.min.js',
        '/c/libs/glitch-canvas.min.js'
      ], function(_, glitch) {

        var elCanvas, anim;

        function glitchMyDesk() {

          $io.arr.all(document.querySelectorAll('.icon img'), function(item) {
            item.style.height = item.offsetHeight + 'px';
            item.style.width = item.offsetWidth + 'px';
          });
          $io.arr.all(document.querySelectorAll('.icon span'), function(item) {
            item.style.height = item.offsetHeight + 'px';
            item.style.width = item.offsetWidth + 'px';
          });
          $io.arr.all(document.querySelectorAll('.icon'), function(item) {
            item.style.height = item.offsetHeight + 'px';
            item.style.width = item.offsetWidth + 'px';
          });

          html2canvas(scope._desktop, {
            //letterRendering: true,
            onrendered: function(canvas) {
              canvas.id = 'html2canvas';
              elCanvas = canvas;
              document.body.appendChild(canvas);

              var ctx = canvas.getContext('2d');
              var my_image_data = ctx.getImageData( 0, 0, canvas.clientWidth, canvas.clientHeight );

              var parameters = {
                amount: 0,
                seed: 0,
                iterations: (Math.random()*20)+2,
                quality: 30
              };

              anim = $loop(function() {
                parameters.seed += 0.01;
                glitch(my_image_data, parameters, function(image_data) {
                  ctx.putImageData(image_data, 0, 0);
                });
              }).play();
            }
          });
        }
        function unglitchMyDesk(e) {
          e.preventDefault();
          //console.log('bye glitch...');
          anim.pause();
          if (elCanvas.parentNode) elCanvas.parentNode.removeChild(elCanvas);
          $el(scope._desktop).off('click touchstart', unglitchMyDesk);
        }
        $el(scope._desktop).on('click touchstart', unglitchMyDesk);
        glitchMyDesk()
      });

    }
  }

  ,'marburg': {

    exec: function(arg, term) {

      var scope = this;

      if (!scope._data.doctor) scope._data.doctor = {};
      scope._data.doctor.marburg = function() {
        //$('#Marburg').remove();
        if (canvas.parentNode) canvas.parentNode.removeChild(canvas);
        cancelAnimationFrame(animID);
        $el(scope._desktop).off('click', marbugClick);
      }

      var canvas = document.createElement('canvas');
      canvas.id = 'Marburg';
      canvas.className = 'virus';
      canvas.style.position = 'absolute';
      canvas.style.zIndex = '9999';
      canvas.style.top = '0';
      canvas.style.left = '0';
      canvas.style.pointerEvents = 'none';
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
      this._everything.appendChild(canvas);
      var context = canvas.getContext('2d');
      context.webkitImageSmoothingEnabled = false;
      context.oImageSmoothingEnabled = false;
      context.mozImageSmoothingEnabled = false;
      context.imageSmoothingEnabled = false;
      //var audioKill = $sound('/c/programs/marburg/killAll.ogg');
      var audioBlop = $sound('/c/sys/sounds/BLOP.ogg');
      marburg = [];
      var numMarburg = 1;
      var marburgKill = 0;
      var marburgKillCount = 0;
      var killAllWave = 0;
      var marbkill = 0;

      function marbugClick() {
        if (MarburgInfect == 1) {
          tempMarburg = new marburgObjet();
          marburg.push(tempMarburg);
          numMarburg = numMarburg + 1;
          if (marburgKill == 0) {
            audioBlop.play();
          };
        };
      }
      $el(scope._desktop).on('click', marbugClick);

      var imageObj = new Image();
      imageObj.onload = function() {};
      imageObj.src = '/c/files/images/png/error-alpha.png';
      animate();

      var animID;
      function animate() {
        animID = requestAnimationFrame(animate);
        if (marburg.length > 0) {
          draw();
        }
      }

      function draw() {
        // CLEAR SCREEN
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
        var i;
        for (i = 0; i < numMarburg; i++) {
          //the drawing of the shape is handled by a function inside the external class.
          //we must pass as an argument the context to which we are drawing the shape.
          if (!marburg[i]) continue;
          marburg[i].myX += Math.floor((Math.random() * 5)) - 2;
          marburg[i].myY += Math.floor((Math.random() * 5)) - 2;
          if (marburg[i].mySize < 10) {
            marburg.splice(i, 1);
            continue;
          };
          if (marburg[i].myRandomSize != marburg[i].mySize) {
            marburg[i].mySize = marburg[i].mySize + (marburg[i].myRandomSize - marburg[i].mySize) / 4;
          };
          context.drawImage(imageObj, marburg[i].myX - marburg[i].mySize / 2, marburg[i].myY - marburg[i].mySize / 2, marburg[i].mySize, marburg[i].mySize);
        }
      }

      function marburgObjet() {
        this.myMaxX = window.innerWidth - 32;
        this.myMaxY = window.innerHeight - 32;
        this.myX = Math.floor((Math.random() * this.myMaxX));
        this.myY = Math.floor((Math.random() * this.myMaxY));
        this.myRandomSize = (Math.floor((Math.random() * 128))) + 32;
        this.mySize = 10;
      }

      function MarbugInfect() {
        MarburgInfect = 1;
        tempMarburg = new marburgObjet();
        marburg.push(tempMarburg);
        numMarburg = numMarburg + 1;
        audioBlop.play();
      };
      MarbugInfect();
  }}

  /////////////////////////////////////////////////////////////////////////////

  // connect
  /////////////////////////////////////////////////////////////////////////////


  /*,'qursor': { // 💨
    //cmd: true,
    exec: function() {

      var scope = this;
      var curmove, curup, curdowm, leftClick = 0, rightClick = 0;
      var users = {};
      var arenaEl = document.createElement('div');
      var userEl = document.createElement('div');
      var aimEl = document.createElement('div');
      arenaEl.className = "app_qursor_arena";
      userEl.className = "app_qursor_arena__user";
      aimEl.className = "app_qursor_arena__aim";

      var me = userEl.cloneNode(false);
      me.innerHTML = 'me';
      me.style.left = '10px';
      me.style.top = '10px';
      arenaEl.appendChild(me);

      var aim = aimEl.cloneNode(false);
      aim.style.left = '10px';
      aim.style.top = '10px';
      arenaEl.appendChild(aim);

      document.body.appendChild(arenaEl);

      var aim_diff_x = -20;
      var aim_diff_y = -30;
      var aimX = 0, aimY = 0;

      var x, y;

      var loop = $loop(function() {
        x = aimX + aim_diff_x;
        y = aimY + aim_diff_y;
        if (x > 0 && x < 600) {
          if ($key('left')) {aim_diff_x -= 10}
          if ($key('right')) {aim_diff_x += 10}
        }
        if (y > 0 && y < 600) {
          if ($key('up')) {aim_diff_y -= 10}
          if ($key('down')) {aim_diff_y += 10}
        }
        aim.style.left = x + 'px';
        aim.style.top = y + 'px';
      });

      loop.play();


      var H = window.innerHeight;
      var W = window.innerWidth;

      $connect(function(session) {

        function sendCursorData(e) {
          e.preventDefault();
          e.stopPropagation();
          e.stopImmediatePropagation();

          aX = e.clientX;
          aY = e.clientY;

          //console.log(aX, W);

          var pX = ((aX / W) * 100);
          var pY = ((aY / H) * 100);

          //console.log(pX, pY);

          if (leftClick) {

            for (var u in users) {
              if (users.hasOwnProperty(u)) {
                //console.log(users[u]);
                var uY = users[u].offsetTop;
                var uX = users[u].offsetLeft;
                //console.log(aY, aX);
                //console.log(uY, uX);

                var intersect = $geo.intersectRect(
                  {left: aY - 16, right: aY + 16, top: aX - 16, bottom: aX + 16},
                  {left: uY - 16, right: uY + 16, top: uX - 16, bottom: uX + 16}
                );

                console.log(intersect);

                if (intersect) {
                  // userEl.className = "app_qursor_arena__user app_qursor_arena__user--fraged";
                  // setTimeout(function() {
                  //   userEl.className = "app_qursor_arena__user";
                  // }, 3000);

                  console.log('Frag : ' + users[u].innerHTML);

                }

              }
            }

          }


          //session.publish('qursor.aim', [e.clientX, e.clientY, leftClick, rightClick]);
          //session.publish('qursor.user', [e.clientX, e.clientY, leftClick, rightClick]);
          session.publish('qursor.user', [pX, pY, leftClick, rightClick]);

          me.style.left = e.clientX + 'px';
          me.style.top = e.clientY + 'px';

        }

        curmove = function (e) {
          sendCursorData(e)
        }
        curup = function (e) {
          var e = e || window.event;
          if ((e.which && e.which == 3)) rightClick = 0
          if ((e.which && e.which == 1)) leftClick = 0;
          sendCursorData(e);
        }
        curdowm = function (e) {
          var e = e || window.event;
          if ((e.which && e.which == 3)) rightClick = 1;
          if ((e.which && e.which == 1)) leftClick = 1;
          sendCursorData(e);
        }
        contextmenu = function (e) {
          e.preventDefault();
          e.stopPropagation();
          e.stopImmediatePropagation();
        }

        session.subscribe('qursor.user', function (msg) {
          var el;
          if (users[msg[0]]) {
            el = users[msg[0]];
            //el.style.left = msg[1] + 'px';
            //el.style.top = msg[2] + 'px';
            el.style.left = msg[1] + '%';
            el.style.top = msg[2] + '%';
          } else {
            el = userEl.cloneNode(false);
            el.innerHTML = msg[0];
            //el.style.left = msg[1] + 'px';
            //el.style.top = msg[2] + 'px';
            el.style.left = msg[1] + '%';
            el.style.top = msg[2] + '%';
            arenaEl.appendChild(el);
            users[msg[0]] = el;
          }
        });

        document.addEventListener('mousedown', curdowm, false);
        document.addEventListener('mouseup', curup, false);
        document.addEventListener('mousemove', curmove, false);
        document.addEventListener('contextmenu', contextmenu, false);

      });

      function destroy() {
        document.removeEventListener('mousedown', curdowm);
        document.removeEventListener('mouseup', curup);
        document.removeEventListener('mousemove', curmove);
        document.removeEventListener('contextmenu', contextmenu);
      }

    }
  }*/

  /*,'chat': { // 💨
    //cmd: true,
    exec: function() {

      var scope = this;
      var cli = scope._states.opened['terminal'].cli;

      //console.log(cli);

      cli.log(' ');
      cli.log.white("Command-line chat loading...");
      cli.log.white("type exit to terminate");

      $connect(function(session) {

        session.subscribe('chat.message', function (msg) {
          cli.log.cyan(msg[0] + ' : ' + $io.str.autolink(msg[1]));
        });

        session.subscribe('apps.login', function (msg) {
          console.log('login', msg);
          //cli.log.cyan(msg[0] + ' is online...');
        });

        cli.onenter = function(str) {
          if (str == 'exit') {
            cli.log.white('bye...');
            destroy();
            return false;
          }

          cli.log.magenta('me : ' + $io.str.autolink(str));
          session.publish('chat.message', [str]);

          return false;
        }

      });

      cli.prompt.innerHTML = 'chat>&nbsp;';
      function destroy() {
        cli.prompt.innerHTML = '>&nbsp;';
        cli.onenter = $noop;
      }

    }
  }*/
  /////////////////////////////////////////////////////////////////////////////

})
