### Immutable vs. Object.assign vs. spread-operator

#### 1. Object.assign

  1.1 Copy staff1 to newStaff1
  
        let staff1 = {title:['manager','sales'],name:'jack',isOn:{in:true}};
        
        let newStaff1 = Object.assign({},staff1);
        
  1.2.*Modify newStaff1:
  
        newStaff1.isOn.in = false;

  1.3.*Output Error
  
        -> staff1.isOn.in = false
        
        -> newStaff1.isOn.in = false
        
![alt tag](https://github.com/lastingyeh/React-MEMO/blob/master/ImmutableMemo/staff1.jpeg)

#### 2. Use Spread-Operator {...}

  2.1 Copy staff2 to new newStaff2
		
        let staff2 = {title:['manager','sales'],name:'jack',isOn:{in:true}};
        
        let newStaff2 = {...staff2};
        
  2.2 *Modify newStaff:
				
	    newStaff2.isOn.in = false;
        
  2.3.*Output Error
  
        -> staff2.isOn.in = false
        
        -> newStaff2.isOn.in = false 
        
![alt tag](https://github.com/lastingyeh/React-MEMO/blob/master/ImmutableMemo/staff2.jpeg)

#### 3. Use Immutable

  3.1 Create Immutable from JS
  
        let staff3 = Immutable.fromJS({title:['manager','sales'],name:'jack',isOn:{in:true}});

  3.2 Modify staff3.isOn.in = false,and it pointed to newStaff3
  
        let newStaff3 = staff3.setIn(['isOn','in'],false);

  3.3 *Back to JS and Output Expected
  
        staff3.toJS() -> staff3.isOn.in = true
        
        newStaff3.toJS() -> newStaff3.isOn.in = false
        
![alt tag](https://github.com/lastingyeh/React-MEMO/blob/master/ImmutableMemo/staff3.jpeg)

#### 4. Summary 

  4.1 Use object.assign || {...} 
      
        -> if you want to modify props of Object deeply 
      
        -> use 'Object.assign({},staff1,isOn:{in:false})' -> correct (when it created)

        -> don't use 'newStaff1.isOn.in = false' -> staff1 modified unexpected indirectly 

  4.2 Use Immutable

        -> Create Immutable Object by fromJS()

        -> Modify and set newObject

        -> Back to object by JS() for use
