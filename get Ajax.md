# Ajax
$( ".tabs-team__title li" ).each(function( index ) {
                 $(".tabs-team__title li .tabs-ttl__1" ).addClass('tab-active')
                 $.ajax({
                url: '/departments/bod',
                type: 'POST',
                success: function (data) {
                    $('.tabs-content__group').find('.tabs-team__content').remove();
                    var result = $('<div />').append(data).find('.tabs-team__content').clone();
                    $('.tabs-content__group .tabs-team__inner').append(result);
                    }
                });
                
                $(this).find('a').on('click', function (e) {
                    var _thisUrl = $(this).attr('href');
                    $(".tabs-team__title li a" ).removeClass('tab-active')
                    $(this).addClass('tab-active')
                  
                $.ajax({
                url: _thisUrl,
                type: 'POST',
                success: function (data) {
                    $('.tabs-content__group').find('.tabs-team__content').remove();
                    var result = $('<div />').append(data).find('.tabs-team__content').clone();
                    $('.tabs-content__group .tabs-team__inner').append(result);
                    }
                });
                
                e.preventDefault();
                })
            });
