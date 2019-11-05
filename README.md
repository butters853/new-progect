<!DOCTYPE html>
<html lang="ru">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <meta name="description" content="2-3 предложения - описание сайта в поисковой системе">
    <meta name="keywords" content="слово, словослово, слово.....">
    <link rel="shortcut icon" href="../img/logokhen1.png" type="image/x-icon">
    <link rel="stylesheet" href="../coffee/style.css">
    <link href="https://fonts.googleapis.com/css?family=Pacifico&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
    <title>Coffee</title>
  </head>
  <body>
      <div class="container">
          <div class="row mt-5">
              <div class="col-6 coffee_list">
                  <div class="coffee_item my-3" onclick="getCoffee(56)">
                      <img src="../coffee/img/Americano321.png" class="rounded-circle">
                      <span> Американо - 56 руб.</span>
                  </div>
                  <div class="coffee_item my-3" onclick="getCoffee(59)">
                      <img src="../coffee/img/Latte321.png" class="rounded-circle">
                      <span> Латте - 59 руб.</span>
                  </div>
                  <div class="coffee_item my-3" onclick="getCoffee(63)">
                      <img src="../coffee/img/Cappuccino321.png" class="rounded-circle">
                      <span> Капучино - 63 руб.</span>
                  </div>
                  <div class="coffee_item my-3" onclick="getCoffee(41)">
                      <img src="../coffee/img/Macchiato.png" class="rounded-circle">
                      <span> Макиато - 41 руб.</span>
                  </div>
                  <div class="coffee_item my-3" onclick="getCoffee(89)">
                      <img src="../coffee/img/Flat_White-ru.svg.png" class="rounded-circle">
                      <span> Флэт уайт - 89 руб.</span>
                  </div>
              </div> 
              <div class="col-6 coffee_oper">
                  <div class="row">
                      <div class="col-6">
                          <div class="display" id="display">
                              <span class="display_text">Выберите кофе</span>
                              <span id="balanceDisplay"></span>
                              <div class="progress mt-3">
                              <div class="progress-bar progress-bar-striped progress-bar-animated" role="progressbar" aria-valuenow="75" aria-valuemin="0" aria-valuemax="100" style="width: 75%">
                              </div>
                              </div>
                          </div>
                          <div class="image">
                          <img src="https://pngimage.net/wp-content/uploads/2018/06/%D0%BA%D0%BE%D1%84%D0%B5%D0%B9%D0%BD%D1%8B%D0%B9-%D1%81%D1%82%D0%B0%D0%BA%D0%B0%D0%BD-png-4.png" alt="">
                          </div>
                      </div>
                      <div class="col-6">
                          <div class="input-group mb-3 balance">
                              <input type="text" class="form-control" id="balance" placeholder="Баланс">
                              <div class="input-group-append">
                                  <span class="input-group-text" id="basic-addon2">руб.</span>
                              </div>
                          </div>
                          <div class="atm">
                              <img id="atm" src="img/bill_acc.png" alt="">
                          </div>
                          <div class="change">
                          </div>
                      </div>
                  </div>
              </div>
          </div>
          <img class="cuper" src="../coffee/img/5rub.jpg" alt="5">
          <img class="cuper" src="../coffee/img/10rub.jpg" alt="10">
          <img class="cuper" src="../coffee/img/50rub.jpg" alt="50">
          <img class="cuper" src="../coffee/img/100rub.jpg" alt="100">
          <img class="cuper" src="../coffee/img/200rub.jpg" alt="200">
          <img class="cuper" src="../coffee/img/500rub.jpg" alt="500">
      </div>
      <script>
          function getCoffee(cost) {
              if (cost<=balance.value) {
                   display.innerText = 'Кофе готов!';
                   balance.value -= cost;
          }
              else 
                  display.innerText = 'Недостаточно средств!';
          }    /* вызываем в событии каждой кнопки функцию, которая считает деньги, относительно
                цены, написанной в инпуте*/
          
          document.onmousedown = function(event) {
              try {
                  if (!event.target.src.endsWith('rub.jpg')) return;  /* вызываем в консоль поисковой результат по концу строки rub.jpg из ссылки купюр, инвертируем значение выражения !
               */
              } catch(error) {
                  return false;
              }
              let bill = event.target;
              bill.ondragstart = function() {   /* отменяет стандартную функцию браузера дроп */
              return false;
              };
              bill.style.position = 'absolute';
              bill.style.zIndex = 10;
              bill.style.transform = "rotate(90deg)"; 
              moveAt(event.pageX, event.pageY);
              function moveAt(pageX, pageY) {
                  bill.style.left = pageX-bill.offsetWidth/2+'px';   /* оцентровка по ширине */
                  bill.style.top = pageY-bill.offsetHeight/2+'px';  /* оцинтровка по высоте */
              }
              function onMouseMove(event) {
              moveAt(event.pageX, event.pageY);
              }
              document.addEventListener('mousemove', onMouseMove);
              bill.onmouseup = function(event) {
              document.removeEventListener('mousemove', onMouseMove);
              bill.style.zIndex = 5;
              bill.onmouseup = null;
              let bill_left  = bill.getBoundingClientRect().left;
              let bill_right = bill_left + bill.getBoundingClientRect().width;
              let bill_top   = bill.getBoundingClientRect().top;
              let atm_left   = atm.getBoundingClientRect().left;
              let atm_right  = atm_left + atm.getBoundingClientRect().width;
              let atm_top    = atm.getBoundingClientRect().top;
              let atm_bottom = atm_top + atm.getBoundingClientRect().height/3;
              if (bill_left > atm_left && bill_right < atm_right && atm_top < bill_top && atm_bottom > atm_top) {
                  bill.style.display = "none";
                  balance.value = +balance.value + +bill.alt;
                  balanceDisplay.innerText = "\n" + "Баланс: " + balance.value;
                  
              }
              
            }
                
          }; 
            
            
      </script>
  <!-- <script>
      let buttons = document.querySelectorAll('.coffee_item');
      let balance = document.querySelector('.balance input');
      console.log(buttons);
      for(let i = 0; i < buttons.length; i++) {
          buttons[i].addEventListener('click', cookCoffee);
      }
  
      function cookCoffee() {
          if (+balance.value <+this.getAttribute('cost')) {
              alert('Недостаточно средств');
              return;
          }
              balance.vale -= this.getAttribute('cost');
      } 
  </script> -->
    <script src="https://code.jquery.com/jquery-3.3.1.slim.min.js" integrity="sha384-q8i/X+965DzO0rT7abK41JStQIAqVgRVzpbzo5smXKp4YfRvH+8abtTE1Pi6jizo" crossorigin="anonymous"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js" integrity="sha384-UO2eT0CpHqdSJQ6hJty5KVphtPhzWj9WO1clHTMGa3JDZwrnQq4sF86dIHNDz0W1" crossorigin="anonymous"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js" integrity="sha384-JjSmVgyd0p3pXB1rRibZUAYoIIy6OrQ6VrjIEaFf/nJGzIxFDsf4x0xIM+B07jRM" crossorigin="anonymous"></script>
  </body>
</html>
