# BootStrap DateTimePicker

```
<script type="text/javascript">
    $(function () {
        var option = {
            sideByside : true
            ...
        }

        $('#datetimepicker1').datetimepicker(options);
    });
</script>
```

```
<div class="container">
    <div class="row">
        <div class='col-sm-6'>
            <div class="form-group">
                <div class='input-group date' id='datetimepicker1'>
                    <input type='text' class="form-control" />
                    <span class="input-group-addon">
                        <span class="glyphicon glyphicon-calendar"></span>
                    </span>
                </div>
            </div>
        </div>
    </div>
</div>
```

datetimepicker()함수 안에 option을 넣으면 datetimepicker에 대해 설정을 정할 수 있다.

format
- date를 "YYYY-MM-DD"처럼 원하는 형식으로 바꿀 수 있다.

sideBySide
- 시간과 날짜를 같이 보면서 설정을 할 수 있다.

showClear
- input을 null로 만들 수 있는 icon이 toolbar에 나타나게 한다.

showClose
- datetimepicker를 사라지게 할 수 있는 hide()함수를 호출하는 icon이 toolbar에 나타나게 한다.

showTodayButton
- calendar에 현재 date를 선택할 수 있는 icon이 toolbar에 나타나게 한다.

toolbarPlacement
- 옵션으로 "top", "bottom"을 주면 toolbar가 datetimepicker의 상단 또는 하단에 나타나게 할 수 있도록 설정할 수 있다.
- sideBySide 옵션을 준 상태에서 toolbarPlacement옵션을 설정하지 않으면 toolbar가 나타나지 않아서 showClear, showClose, showTodayButton 옵션으로 설정한 icon들이 보이지 않는다.

참조
[bootstrap_datetimepicker](https://eonasdan.github.io/bootstrap-datetimepicker/)
