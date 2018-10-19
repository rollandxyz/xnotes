```js
import { FormControl, ValidatorFn, Validators } from '@angular/forms';

ngOnInit() {
    this.workDefPayloadFields = this.service.getPayloadFields();

    const unamePattern = '^[a-z0-9_-]{8,15}$';
    const pwdPattern = '^(?=.*\d)(?=.*[a-z])(?=.*[A-Z])(?!.*\s).{6,12}$';
    const mobnumPattern = '^((\\+91-?)|0)?[0-9]{10}$';
    const emailPattern = '^[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,4}$';


    this.testCase_0();

    console.log('------------');
    this.testCase_1();

    console.log('------------');
    this.testCase_2();

    console.log('------------');
    this.testUserName();
  }

  testUserName() {
    const myControl = new FormControl('', this.validateUserNameFn());

    myControl.setValue(''); // Control is invalid.
    myControl.updateValueAndValidity();
    console.error(`valid=${myControl.valid}, errors=${myControl.errors}`, myControl.errors);

    myControl.setValue('q12'); // Control is invalid.
    myControl.updateValueAndValidity();
    console.error(`valid=${myControl.valid}, errors=${myControl.errors}`, myControl.errors);

    myControl.setValue('*&^%qt5567iii'); // Control is invalid.
    myControl.updateValueAndValidity();
    console.error(`valid=${myControl.valid}, errors=${myControl.errors}`, myControl.errors);

    myControl.setValue('1234567890d'); // Control is invalid.
    myControl.updateValueAndValidity();
    console.log(`valid=${myControl.valid}, errors=${myControl.errors}`, myControl.errors);

    myControl.setValue('abc'); // Control is invalid.
    myControl.updateValueAndValidity();
    console.error(`valid=${myControl.valid}, errors=${myControl.errors}`, myControl.errors);

    myControl.setValue('abcwwwwwwwwwwwwwwwwwoooooooooooowwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwww'); // Control is invalid.
    myControl.updateValueAndValidity();
    console.error(`valid=${myControl.valid}, errors=${myControl.errors}`, myControl.errors);

    myControl.setValue('sdqw123456'); // Control is invalid.
    myControl.updateValueAndValidity();
    console.log(`valid=${myControl.valid}, errors=${myControl.errors}`, myControl.errors);
  }
  validateUserNameFn() {
    const validators: Array<ValidatorFn> = [];
    validators.push(Validators.required);
    validators.push(Validators.minLength(5));
    validators.push(Validators.maxLength(25));
    validators.push(Validators.pattern('^(?=.*[a-zA-Z])(?=.*[0-9])[a-zA-Z0-9]+$'));
    const compValidatorFn = Validators.compose(validators);
    return compValidatorFn;
  }

  testCase_2() {

    const myControl = new FormControl('initialValue', this.validatorLengthFn(5, 10));

    myControl.setValue(''); // Control is invalid.
    myControl.updateValueAndValidity();
    console.error(`valid=${myControl.valid}, errors=${myControl.errors}`, myControl.errors);

    myControl.setValue('12'); // Control is invalid.
    myControl.updateValueAndValidity();
    console.error(`valid=${myControl.valid}, errors=${myControl.errors}`, myControl.errors);

    myControl.setValue('12345'); // Control is invalid.
    myControl.updateValueAndValidity();
    console.log(`valid=${myControl.valid}, errors=${myControl.errors}`, myControl.errors);

    myControl.setValue('12345456'); // Control is invalid.
    myControl.updateValueAndValidity();
    console.log(`valid=${myControl.valid}, errors=${myControl.errors}`, myControl.errors);

    myControl.setValue('12345678901234'); // Control is valid.
    myControl.updateValueAndValidity();
    console.error(`valid=${myControl.valid}, errors=${myControl.errors}`, myControl.errors);
  }
  testCase_1() {
    const lnPattern = '[1-9]{5}';
    const myControl = new FormControl('initialValue', this.validatePatternFn(lnPattern));

    myControl.setValue('12'); // Control is invalid.
    myControl.updateValueAndValidity();
    console.error(`valid=${myControl.valid}, errors=${myControl.errors}`, myControl.errors);

    myControl.setValue('012345689'); // Control is invalid.
    myControl.updateValueAndValidity();
    console.error(`valid=${myControl.valid}, errors=${myControl.errors}`, myControl.errors);

    myControl.setValue('12345'); // Control is invalid.
    myControl.updateValueAndValidity();
    console.log(`valid=${myControl.valid}, errors=${myControl.errors}`, myControl.errors);

    myControl.setValue('qb'); // Control is valid.
    myControl.updateValueAndValidity();
    console.error(`valid=${myControl.valid}, errors=${myControl.errors}`, myControl.errors);
  }
  testCase_0() {
    const lnPattern = '[a-z]{2}';
    const myControl = new FormControl('initialValue', this.validatePatternFn(lnPattern));

    myControl.setValue('12'); // Control is invalid.
    myControl.updateValueAndValidity();
    console.error(`valid=${myControl.valid}, errors=${myControl.errors}`, myControl.errors);

    myControl.setValue('012345689'); // Control is invalid.
    myControl.updateValueAndValidity();
    console.error(`valid=${myControl.valid}, errors=${myControl.errors}`, myControl.errors);

    myControl.setValue('qb'); // Control is valid.
    myControl.updateValueAndValidity();
    console.log(`valid=${myControl.valid}, errors=${myControl.errors}`, myControl.errors);
  }

  validatorLengthFn(minLen: number, maxLen: number): any {
    const validators: Array<ValidatorFn> = [];
    validators.push(Validators.required);
    validators.push(Validators.minLength(minLen));
    validators.push(Validators.maxLength(maxLen));
    const compValidatorFn = Validators.compose(validators);
    return compValidatorFn;
  }

  validatePatternFn(pattern: string): any {
    const validators: Array<ValidatorFn> = [];
    validators.push(Validators.required);
    validators.push(Validators.pattern(pattern));
    const compValidatorFn = Validators.compose(validators);
    return compValidatorFn;
  }
  ```
