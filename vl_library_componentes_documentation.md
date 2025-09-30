# Documentación de Librerías VL-NGX y VL-NGX-Business

## Información General

### vl-ngx
- **Versión**: ~17.0.149
- **Descripción**: Librería core de componentes Angular para Visma Latam
- **Repositorio**: Azure DevOps (vismalatam.frontend.libraries)

### vl-ngx-business  
- **Versión**: 17.0.16
- **Descripción**: Librería de componentes de negocio específicos para aplicaciones HR
- **Repositorio**: Azure DevOps (vismalatam.frontend.libraries)

---

## VL-NGX - Componentes Core

### 🔸 Componentes de Interfaz

#### VlNgxAlertComponent
```typescript
import { VlNgxAlertComponent } from "vl-ngx/components/alert";
```
**Uso en HTML:**
```html
<vl-ngx-alert [id]="'alert-id'"></vl-ngx-alert>
```
**Funcionalidad**: Componente para mostrar alertas y mensajes informativos
**Servicios asociados**: `VlNgxAlertService`

#### VlNgxButtonComponent
```typescript
import { VlNgxButtonComponent } from "vl-ngx/components/button";
```
**Uso en HTML:**
```html
<vl-ngx-button 
  [color]="'secondary'" 
  [size]="'regular'" 
  [disabled]="false"
  [outlined]="true"
  [icon]="buttonIcon"
  (click)="action()">
  Texto del botón
</vl-ngx-button>
```
**Propiedades**:
- `color`: 'primary' | 'secondary' | 'light'
- `size`: 'small' | 'regular' | 'large'
- `disabled`: boolean
- `outlined`: boolean
- `icon`: VlNgxButtonIcon

#### VlNgxSelectComponent
```typescript
import { VlNgxSelectComponent } from "vl-ngx/components/select";
```
**Uso en HTML:**
```html
<vl-ngx-select
  [items]="selectItems"
  [placeholder]="'Seleccionar...'"
  [(ngModel)]="selectedValue">
</vl-ngx-select>
```

#### VlNgxSpinnerComponent
```typescript
import { VlNgxSpinnerComponent, VlNgxSpinnerService } from "vl-ngx/components/spinner";
```
**Uso en HTML:**
```html
<vl-ngx-spinner [id]="spinnerName"></vl-ngx-spinner>
```
**Servicio**: Control programático con `VlNgxSpinnerService`

#### VlNgxModalComponent
```typescript
import { VlNgxModalComponent } from "vl-ngx/components/modal";
```
**Servicios asociados**: 
- `VlNgxModalService`
- `ModalData` (modelo)

#### VlNgxTableComponent
```typescript
import { VlNgxTableComponent } from "vl-ngx/components/grid/table";
```
**Servicios asociados**: `VlNgxTableService`
**Modelos relacionados**:
- `VlNgxHeader`
- `VlNgxTableProperties`
- `VlNgxSort`
- `VlNgxPagingMode`
- `VlNgxAlign`

### 🔸 Componentes Especializados

#### VlNgxEllipsisComponent
```typescript
import { VlNgxEllipsisComponent } from "vl-ngx/components/ellipsis";
```
**Uso en HTML:**
```html
<vl-ngx-ellipsis [actions]="ellipsisActions" [element]="item"></vl-ngx-ellipsis>
```
**Modelos**: 
- `VlNgxEllipsis`
- `VlNgxIconTypes`

#### VlNgxDropDownComponent
```typescript
import { VlNgxDropDownComponent } from "vl-ngx/components/drop-down";
```

#### VlNgxPopOverComponent
```typescript
import { VlNgxPopOverComponent } from "vl-ngx/components/pop-over";
```

#### VlNgxFormFooterComponent
```typescript
import { VlNgxFormFooterComponent } from "vl-ngx/components/form-footer";
```
**Uso en HTML:**
```html
<vl-ngx-form-footer [requiredField]="true">
  <!-- Contenido del footer -->
</vl-ngx-form-footer>
```

#### VlNgxHttpStatusMessageComponent
```typescript
import { VlNgxHttpStatusMessageComponent } from "vl-ngx/components/feedbacks/http-status-message";
```

### 🔸 Componentes de Confirmación

#### VlNgxConfirmationService
```typescript
import { VlNgxConfirmationService } from "vl-ngx/components/confirmation";
```
**Modelos**:
- `VlNgxConfirmation`
- `VlNgxConfirmationImage`
- `VlnxConfirmationButtons`

### 🔸 Componentes de Notificación

#### VlNgxSnackbarService
```typescript
import { VlNgxSnackbarService } from "vl-ngx/components/snackbar";
```
**Modelos**: `SnackbarMessage`

### 🔸 Componentes de Navegación

#### VlNgxBreadCrumbService
```typescript
import { VlNgxBreadCrumbService } from "vl-ngx/components/breadcrumb";
```

### 🔸 Componentes de Chips

#### VlNgxChipsService
```typescript
import { VlNgxChipsService } from "vl-ngx/components/chips";
```
**Modelos**: `VlNgxChip`

---

## 🔧 Directivas

### VlNgxFormFieldValidationsDirective
```typescript
import { VlNgxFormFieldValidationsDirective } from "vl-ngx/directives/form-field";
```

### VlNgxPopOverDirective
```typescript
import { VlNgxPopOverDirective } from "vl-ngx/directives/pop-over";
```

### FormSkeletonDirective
```typescript
import { FormSkeletonDirective } from "vl-ngx/directives/skeleton";
```

---

## 🔄 Pipes

### VlNgxTranslatePipe y VlNgxTranslateModule
```typescript
import { VlNgxTranslateModule, VlNgxTranslatePipe } from "vl-ngx/pipes/translate";
```
**Uso en template**:
```html
{{ 'text_key' | translate }}
```

### VlNgxDatePipe
```typescript
import { VlNgxDatePipe } from "vl-ngx/pipes/date";
```
**Modelos**: 
- `VlNgxDateTimeFormats`
- `VlNgxGridDateTimePipe`

---

## 🎨 Views (Vistas Complejas)

### VlNgxLeftPanelDashboardComponent
```typescript
import { VlNgxLeftPanelDashboardComponent } from "vl-ngx/views/dashboard/left-panel";
```
**Uso en HTML:**
```html
<vl-ngx-left-panel-dashboard>
  <!-- Contenido del dashboard -->
</vl-ngx-left-panel-dashboard>
```

### VlNgxStepperComponent
```typescript
import { VlNgxStepperComponent } from "vl-ngx/views/stepper";
```
**Uso en HTML:**
```html
<vl-ngx-stepper 
  [forms]="forms" 
  [isLinear]="true" 
  (stepSaved)="continue($event)" 
  [(goToNextStep)]="goToNextStep">
</vl-ngx-stepper>
```

### VlNgxFormContainerComponent
```typescript
import { VlNgxFormContainerComponent } from "vl-ngx/views/form";
```

### VlNgxGridBasicComponent
```typescript
import { VlNgxGridBasicComponent } from "vl-ngx/views/grid";
```

### VlNgxDropDownFilterDateTimeComponent
```typescript
import { VlNgxDropDownFilterDateTimeComponent } from "vl-ngx/views/filters/drop-down-date-time";
```

---

## 🔨 Servicios

### VlNgxTranslateService
```typescript
import { VlNgxTranslateService } from "vl-ngx/pipes/translate";
```

### VlNgxSettingsService
```typescript
import { VlNgxSettingsService } from "vl-ngx/services/settings";
```
**Modelos**: `VlNgxSettings`

### VlNgxExcelService
```typescript
import { VlNgxExcelService } from "vl-ngx/services/excel";
```

---

## 🎯 Adaptadores y Proveedores

### VlNgxCustomDateAdapter
```typescript
import { VlNgxCustomDateAdapter } from "vl-ngx/adapters";
```

### Proveedores de Configuración
```typescript
import { VLNGX_MAT_RIPPLE } from "vl-ngx/providers";
import { 
  VLNGX_DATE_PIPE_DEFAULT_OPTIONS, 
  VLNGX_MAT_DATE_LOCALE,
  VlNgxRegisterLocaleDataFunction 
} from "vl-ngx/providers/date-settings";
```

---

## 📊 Modelos y Enums

### VlNgxShapes
```typescript
import { 
  VlNgxDisplayShapeImage, 
  VlNgxShapeIcons 
} from "vl-ngx/components/shapes/models";
```

### Iconografía y Enums
```typescript
import { 
  VlNgxActionIcons,
  VlNgxFormIcons,
  VlNgxIllustratedIcons,
  VlNgxIllustrations 
} from "vl-ngx/utils/enums";
```

---

## VL-NGX-Business - Componentes de Negocio

### 🏢 Componentes Organizacionales

#### TreeComponent
```typescript
import { TreeComponent } from "vl-ngx-business/components/tree";
```
**Uso en HTML:**
```html
<vl-ngx-business-tree [treeNode]="treeNode"></vl-ngx-business-tree>
```
**Modelos**: `TreeNode`

#### EmployeeSummaryComponent
```typescript
import { EmployeeSummaryComponent } from "vl-ngx-business/components/employee-summary";
```
**Uso en HTML:**
```html
<vl-ngx-business-employee-summary 
  [summaryType]="summaryType"
  [employeeId]="employeeId">
</vl-ngx-business-employee-summary>
```
**Modelos**: 
- `SummaryTypeEnum`
- `EmployeeSummaryState`

### 🎯 Componentes de Drag and Drop

#### DragAndDropEmployeeComponent
```typescript
import { DragAndDropEmployeeComponent } from "vl-ngx-business/components/drag-and-drops";
```
**Uso en HTML:**
```html
<vl-ngx-business-drag-and-drop-employee
  [selectedEmployees]="selectedEmployees"
  (employeesChanged)="onEmployeesChanged($event)">
</vl-ngx-business-drag-and-drop-employee>
```
**Modelos**:
- `DragAndDropEmployeeOptions`
- `DragAndDropEmployeeState`
- `DragAndDropEmployeeEvents`

---

## 🔧 Servicios de Negocio

### AuthService
```typescript
import { AuthService } from "vl-ngx-business/services/core";
```

### UserService
```typescript
import { UserService } from "vl-ngx-business/services/core";
```

### EmployeeSearchService
```typescript
import { EmployeeSearchService } from "vl-ngx-business/services/hrcore";
```

---

## 📋 Modelos de Datos

### API Configuration
```typescript
import { API_CONFIG, ApiConfig } from "vl-ngx-business/models/api";
```

### Core Models
```typescript
import { 
  PageFilter, 
  PaginatedList,
  SelectItem 
} from "vl-ngx-business/models/core";
```

### GraphQL Models
```typescript
import { 
  EmployeeSearchFilter,
  EmployeeSearchResult,
  EmployeeFilterParameters,
  EmployeeResult,
  ContractFilter,
  DataLocationEnum,
  EmployeeSearchAdditionalData
} from "vl-ngx-business/models/graphql";
```

### Organization Models
```typescript
import { 
  StructureFilter,
  PhaseFilter 
} from "vl-ngx-business/models/organization";
```

### HR Core Models
```typescript
import { EntityType } from "vl-ngx-business/models/hrcore";
```

---

## 💡 Patrones de Uso Comunes

### 1. Configuración de Tabla con Grid
```typescript
// Configuración típica de una tabla
public readonly tableProperties: VlNgxTableProperties = {
  headers: this.headers,
  data: this.data,
  pagingMode: VlNgxPagingMode.Server,
  sort: this.sort
};
```

### 2. Uso de Spinner con ID único
```typescript
public readonly spinnerId = "vl-ngx-grid-processing";

// En el servicio
this._spinnerService.show(this.spinnerId);
this._spinnerService.hide(this.spinnerId);
```

### 3. Configuración de Alertas
```typescript
// Inyectar servicio
constructor(private _alertService: VlNgxAlertService) {}

// Mostrar alerta
this._alertService.showInfo("mensaje-id", "Mensaje de información");
```

### 4. Manejo de Modales
```typescript
// Abrir modal
const modalData: ModalData = {
  component: ComponenteModal,
  data: this.dataToPass
};
this._modalService.open(modalData);
```

---

## 🎨 Temas y Estilos

### Colores de Botones
- `primary`: Color principal del tema
- `secondary`: Color secundario
- `light`: Color claro/neutro

### Tamaños
- `small`: Tamaño pequeño
- `regular`: Tamaño estándar
- `large`: Tamaño grande

---

## 📚 Ejemplos de Implementación

### Ejemplo: Formulario con Validaciones
```html
<vl-ngx-form-container>
  <form [formGroup]="myForm">
    <vl-ngx-select 
      formControlName="selection"
      vlNgxFormFieldValidations
      [items]="selectItems">
    </vl-ngx-select>
    
    <vl-ngx-form-footer [requiredField]="true">
      <vl-ngx-button 
        [disabled]="!myForm.valid"
        (click)="submit()">
        Guardar
      </vl-ngx-button>
    </vl-ngx-form-footer>
  </form>
</vl-ngx-form-container>
```

### Ejemplo: Dashboard con Panel Lateral
```html
<vl-ngx-left-panel-dashboard>
  <div slot="left-panel">
    <vl-ngx-business-employee-summary
      [employeeId]="selectedEmployeeId">
    </vl-ngx-business-employee-summary>
  </div>
  
  <div slot="main-content">
    <!-- Contenido principal -->
  </div>
</vl-ngx-left-panel-dashboard>
```

---

## 🔗 Dependencias y Configuración

### Instalación
```json
{
  "dependencies": {
    "vl-ngx": "~17.0.149",
    "vl-ngx-business": "17.0.16"
  }
}
```

### Scripts de Desarrollo
```json
{
  "scripts": {
    "link-ngx": "npm unlink vl-ngx && npm link vl-ngx && cmd /c wait-for-preservesymlinks.bat",
    "link-ngx-business": "npm unlink vl-ngx-business && npm link vl-ngx-business && cmd /c wait-for-preservesymlinks.bat",
    "link-multi-library": "npm unlink vl-ngx vl-ngx-business && npm link vl-ngx vl-ngx-business && cmd /c wait-for-preservesymlinks.bat && npm start"
  }
}
```

---

## 📄 Notas Importantes

1. **Compatibilidad**: Ambas librerías están diseñadas para Angular 17
2. **Repositorio**: Alojadas en Azure DevOps de Visma Latam
3. **Nomenclatura**: Usar PascalCase para imports y kebab-case en HTML
4. **Servicios**: Muchos componentes tienen servicios asociados para control programático
5. **Internacionalización**: Soporte completo con VlNgxTranslateService y pipes
6. **Theming**: Sistema de temas integrado con Material Design

---

*Documentación generada el 29 de septiembre de 2025*
*Basada en el análisis del proyecto VLFrontEndPeople*