# MVW framework없이 Single Page App 만들기 4

***

## COMPONENT 구현

 - Data변경에 따른 Dom제어 및 EventHandler연결 제공
 - 특정 단위의 DOM Tree 선언 편이제공
 - 특정 UI의 시나리오가 반영되지 않은 범용적으로 사용할 수 있는 기능만을 공통으로 구현
 
##### 1. 컴포넌트 생성 - 컴포넌트 모듈에서 생성자를 제공한다. 
 
    objTable = new cmpBasic.table({
        'class' : 'table-protocols',
        'tableHead' : ['Aplicação', 'Porta'],
        'tableData' : [['HTTP', '80'], ['FTP', '21']]
    });
    
##### 2. 컴포넌트 API를 통해 EventHandler연결, Data Get, Set등을 제공한다.

    objForm.setSubmitHandler(function(event) {
        srvService.deleteAllPortForwardingRules();
        event.preventDefault();
    });
    
    objForm.setValueWithId('input', SETUP_TAG_ID, data.destination);
    
##### 3. DOM Tree연결은 생성한 컴포넌트의 최상위 요소인 $element를 통해서 연결하도록 구현.

    if (objForm) {
        $collumnLeftBox.append(objForm.$element);
    }