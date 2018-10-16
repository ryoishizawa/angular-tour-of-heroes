# How to refer to Angular Tutorial "Tour of Heroes"

## Who can read this document
* People who read [Angular Titorial][6906d4cf] can refer to this memo for reviewing your understanding while reading source code.
  - This doc is for the people who is not familiar with Angular yet.
* The provide all source codes [here][a6febc9a].
  - While you're creating new application with Angular, check this for reference.

  [6906d4cf]: https://angular.io/tutorial "Angular Titorial"
  [a6febc9a]: https://stackblitz.com/angular/vvxldjlmnna?file=src%2Fapp%2Fdashboard%2Fdashboard.component.html "Angular Example"

## Start
* The application starts from `index.html`.
* For `<app-root>`, go to `app.component.ts` and there's selector `app-root`.
  - Angular connects component like this.
  - You can also see `app.component.html` and there's basis page.
* `app-routing.module.ts` is for Routing. Here you can see URL and know where to redirect.
  - If there's no path, redirect to `/dashboard`.
  - The following code is an example.

```
const routes: Routes = [
  { path: '', redirectTo: '/dashboard', pathMatch: 'full' },
  { path: 'dashboard', component: DashboardComponent },
  { path: 'detail/:id', component: HeroDetailComponent },
  { path: 'heroes', component: HeroesComponent }
];
```

## Move from dashboard to detail page
* There's link in `dashboard.component.html`: `routerLink="/detail/{{hero.id}}"`
