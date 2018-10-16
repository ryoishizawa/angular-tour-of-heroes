# Angular Tips

## When you'd like to bind data
* Use `@Input`
* Refer to [here][1bd174d0] to understand how to use this.
* The following is the sample:
* HTML
```
<app-detail-pagination index="1" total="15" total_suffix="Records"></app-detail-pagination>
```
* TypeScript
```
export class DetailPaginationComponent implements OnInit {
  @Input() index: number;
  @Input() total: number;
  @Input() total_suffix: string;

  ...
}
```

  [1bd174d0]: https://angular.io/api/core/Input "Angular Input"


## Use brackets
### In HTML
* `[]`: When you call method from HTML.
* `{{}}`: When you use variables from TypeScript.
* (Edit later)
* [Tamplate Syntax][23ae3bb2] page should be helpful.

  [23ae3bb2]: https://angular.io/guide/template-syntax "Angular - Tamplate Syntax"
