---
description: Select component for Universal Dashboard
---

# Select

Select components are used for collecting user provided information from a list of options.

## Simple Select

Create a simple select with multiple options.

![](../../../../.gitbook/assets/image%20%2866%29.png)

```text
New-UDSelect -Option {
    New-UDSelectOption -Name 'One' -Value 1
    New-UDSelectOption -Name 'Two' -Value 2
    New-UDSelectOption -Name 'Three' -Value 3
}
```

## Grouped Select

Create a select with groups of selections.

![](../../../../.gitbook/assets/image%20%2850%29.png)

```text
New-UDSelect -Option {
    New-UDSelectGroup -Name 'Group One' -Option {
        New-UDSelectOption -Name 'One' -Value 1
        New-UDSelectOption -Name 'Two' -Value 2
        New-UDSelectOption -Name 'Three' -Value 3
    }
    New-UDSelectGroup -Name 'Group Two' -Option {
        New-UDSelectOption -Name 'Four' -Value 4
        New-UDSelectOption -Name 'Five' -Value 5
        New-UDSelectOption -Name 'Size' -Value 6
    }
}
```

## OnChange

Execute a PowerShell event handler when the value of the select is changed.

```text
New-UDSelect -Option {
    New-UDSelectOption -Name 'One' -Value 1
    New-UDSelectOption -Name 'Two' -Value 2
    New-UDSelectOption -Name 'Three' -Value 3
} -OnChange { Show-UDToast -Message $EventData }
```

## Get-UDElement

Retrieve the value of the select from another component.

```text
  New-UDSelect -Option {
      New-UDSelectOption -Name 'One' -Value 1
      New-UDSelectOption -Name 'Two' -Value 2
      New-UDSelectOption -Name 'Three' -Value 3
  } -Id 'select' -DefaultValue 2

  New-UDButton  -Text 'OnBoard' -OnClick {
    $Element = Get-UDElement -Id 'select'
    if ($Element.Value)
    {
      Show-UDToast -Message $Element.Value
    }
    else 
    {
      Show-UDToast -Message $Element.DefaultValue
    }
  }
```

**New-UDSelect**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | String | The ID of the component. It defaults to a random GUID. | false |
| Option | ScriptBlock | Options to include in this select. This can be either New-UDSelectOption or New-UDSelectGroup. | false |
| Label | String | The label to show with the select. | false |
| OnChange | Endpoint | A script block that is executed when the script changes. $EventData will be an array of the selected values. | false |
| DefaultValue | String | The default selected value. | false |
| Disabled | SwitchParameter | Whether this select is disabled. | false |
| Multiple | SwitchParameter | Whether you can select multiple values. | false |

