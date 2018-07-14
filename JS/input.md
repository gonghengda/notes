
受控模式下 input rerender 造成光标位置丢失
这个没法在组件层面修复，需要用户在 onchange 里实现，我自己在 2.0 上尝试写了一个demo，希望对大家有帮助，1.x 解决方案类似：

onPhoneChange = (value) => {
    const phoneRef = this.phone.inputRef.inputRef;
    let before = phoneRef.selectionStart;
    this.setState({
      phoneValue: value,
    }, () => {
      const after = phoneRef.selectionStart;
      const subValue = value.substr(before - 1, before);
      if (before !== after) {
        if (subValue && subValue.substr(0, 1) === ' ') {
          before = before + 1;
        }
        phoneRef.setSelectionRange(before, before);
      }
    })
  }
  
