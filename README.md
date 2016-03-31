#Tutorial para la creación de un módulo en Odoo
---------------------------------------------------------------------------------------------------------------------------------------------------------------------
##Os presentamos un tutorial rápido y sencillo para crear un módulo y utilizarlo en la plataforma Odoo.

Para poder trabajar sobre estos módulo se necesitan tres programas base:

--> Virtual Box.

--> Netbeans.

--> Putty.

En estos casos va a ser necesario la configuración de una máquina virtual para implementar Odoo y poder trabajar con él, ¡Pero no te preocupes!, existen máquinas virtuales ya configuradas con este propósito, y en el caso de Odoo son las llamadas “Turnkey”. Para este tutorial usaremos la “Turnkey Postgresql”.

Después de esta breve introducción comenzamos con el trabajo, 
###¿Preparados?

------------------------------------Pasos a seguir para la creación del módulo:------------------------------------------------------------------------

Comenzamos lanzando la máquina virtual para la obtención de direcciones para diferentes tipos de conexión:

![**](https://github.com/Ruben29/ModuloOdoo/blob/master/openacademy/img/1.jpg)

Nada más conseguir nuestra dirección IP ejecutaremos Putty para el lanzamiento de Odoo. Aquí tendremos que introducir la dirección IP y el puerto que nos proporciona la máquina virtual en los dos primeros cuadros.

![**](https://github.com/Ruben29/ModuloOdoo/blob/master/openacademy/img/2%20(2).jpg)

En cuanto lo lancemos, nos pedirá un usuario y contraseña, en nuestro caso serían “root” y “castelao” respectivamente.

![**](https://github.com/Ruben29/ModuloOdoo/blob/master/openacademy/img/3.jpg)

A continuación se introducirán los comandospara lanzar Odoo:

##cd /opt/oddo → ./oddo.py

![**](https://github.com/Ruben29/ModuloOdoo/blob/master/openacademy/img/4.jpg)

Con todo esto lanzado y funcionando a la perfección, recibiremos el puerto necesario para acceder desde el proyecto que crearemos a continuación en Netbeans, como desde el navegador, en este caso es el “8069”.



Ahora vamos a hacer una prueba para ver que todo va bien. Desde el navegador, en nuestro caso Chrome, introduciremos la siguiente ruta:

##https://10.0.160.112:8069


Al ser la primera vez que entramos nos pedirá que creemos una base de datos, escojamos el idioma y la descarga opcional, pero recomendables, archivos iniciales. Otra cosa importante es registrarnos en Odoo con un e-mail para así confirmar la base de datos y que no nos la eliminen.

Si todo esto ha funciona bien nos encontraremos con un resultado de este estilo:

![**](https://github.com/Ruben29/ModuloOdoo/blob/master/openacademy/img/5.jpg)

En otra consola de Putty vamos a instalar un modulo de prueba que posteriormente descargaremos al proyecto que creemos en NetBeans. Usaremos este comando:
##odoo.py scaffold openacademy addons
esto creará una estructura cuya carpeta principal sera openacademy y estará situada en addons.

Paso seguido, procederemos a crear el proyecto en Netbeans. Para esto necesitaremos crear archivos PHP y Python, por lo que si no lo tienes instalado haz lo siguiente:

Tools → Plugins → Available Plugins → Seleccionas los que en “Category” tengan extensión PHP y Python → Install

En cuanto lo tengas procede con la creación del proyecto.

New Project → PHP / PHP Application from Remote Server → Next

Le pondremos el nombre y la ruta donde queremos que nos lo cree → Next

A continuación, procederemos con algunos cambios en la ventana “Remote Connection”

En “Project URL:” pondremos la IP que hemos usado anteriormente “https://10.0.160.112:8069”

En la pestaña “Manage” la dejaremos de la siguiente manera:

![**](https://github.com/Ruben29/ModuloOdoo/blob/master/openacademy/img/6.jpg)

Haremos un test previo para ver si hace la conexión, para ello presionaremos en “Test Connection”.

Un apunte muy importante es que deberemos enviar el módulo a una ruta concreta “sftp://10.0.160.112/opt/odoo/addons” ya que si no Odoo no los reconocerá.

En la siguiente ventana nos proporcionarán muchas carpetas que seleccionar y bajar, pero solo seleccionaremos una “openacademy”, ya que es nuestra guía para hacer nuestro propio módulo.


Ahora ya es momento de trabajar con los archivos del projecto. Lo primero es dejar una estructuración en el programa, es la siguiente: 

![**](https://github.com/Ruben29/ModuloOdoo/blob/master/openacademy/img/7.jpg)

Es hora de ir rellenando los archivos, paso a paso para crear un buen tema.

##ADVERTENCIA
Durante el eguimiento del tutorial se colocará el siguiente mensaje 
##"EL TRAPO!!!"
Este mensaje servira para recordar que debemos ir haciendo **Upload** a la carpeta **openacademy** del proyecto para subirla y actualizarlo en Odoo.
Tambien tendremos que actualizar el modulo en las aplicaciones en linea. Si al actualizar nos dan errores podemos con la consola de PUTTY, con la que arrancamos Odoo, comprobar los fallos. Ademas si no da fallos pero no vemos cambios ya hemos visto que una posible solucion es volver a instalar el **website builder** y el **modulo**. 
  

El primero será el archivo “__openerp__.py”, borraremos lo que tiene dentro por defecto e introduciremos esto:

```java
# -*- coding: utf-8 -*-
{
    'name': "Open Academy",

    'summary': """Manage trainings""",

    'description': """
        Open Academy module for managing trainings:
            - training courses
            - training sessions
            - attendees registration
    """,

    'author': "My Company",
    'website': "http://www.yourcompany.com",

    # Categories can be used to filter modules in modules listing
    # Check https://github.com/odoo/odoo/blob/master/openerp/addons/base/module/module_data.xml
    # for the full list
    'category': 'Test',
    'version': '0.1',

    # any module necessary for this one to work correctly
    'depends': ['base'],

    # always loaded
    'data': [
        # 'security/ir.model.access.csv',
        'templates.xml',
    ],
    # only loaded in demonstration mode
    'demo': [
        'demo.xml',
    ],
}`
```

**openacademy/init.py**

```java
# -*- coding: utf-8 -*-
from . import controllers
from . import models`

**openacademy/controllers.py**

`# -*- coding: utf-8 -*-
from openerp import http

# class Openacademy(http.Controller):
#     @http.route('/openacademy/openacademy/', auth='public')
#     def index(self, **kw):
#         return "Hello, world"

#     @http.route('/openacademy/openacademy/objects/', auth='public')
#     def list(self, **kw):
#         return http.request.render('openacademy.listing', {
#             'root': '/openacademy/openacademy',
#             'objects': http.request.env['openacademy.openacademy'].search([]),
#         })

#     @http.route('/openacademy/openacademy/objects/<model("openacademy.openacademy"):obj>/', auth='public')
#     def object(self, obj, **kw):
#         return http.request.render('openacademy.object', {
#             'object': obj
#         })
```

**demo.xml:**

```java
<openerp>
    <data>
        <!--  -->
        <!--   <record id="object0" model="openacademy.openacademy"> -->
        <!--     <field name="name">Object 0</field> -->
        <!--   </record> -->
        <!--  -->
        <!--   <record id="object1" model="openacademy.openacademy"> -->
        <!--     <field name="name">Object 1</field> -->
        <!--   </record> -->
        <!--  -->
        <!--   <record id="object2" model="openacademy.openacademy"> -->
        <!--     <field name="name">Object 2</field> -->
        <!--   </record> -->
        <!--  -->
        <!--   <record id="object3" model="openacademy.openacademy"> -->
        <!--     <field name="name">Object 3</field> -->
        <!--   </record> -->
        <!--  -->
        <!--   <record id="object4" model="openacademy.openacademy"> -->
        <!--     <field name="name">Object 4</field> -->
        <!--   </record> -->
        <!--  -->
    </data>
</openerp>
```

**models.py:**

```java
# -*- coding: utf-8 -*-

from openerp import models, fields, api

# class openacademy(models.Model):
#     _name = 'openacademy.openacademy'

#     name = fields.Char()
```

**templates.xml:**

```java
<openerp>
    <data>
        <!-- <template id="listing"> -->
        <!--   <ul> -->
        <!--     <li t-foreach="objects" t-as="object"> -->
        <!--       <a t-attf-href="{{ root }}/objects/{{ object.id }}"> -->
        <!--         <t t-esc="object.display_name"/> -->
        <!--       </a> -->
        <!--     </li> -->
        <!--   </ul> -->
        <!-- </template> -->
        <!-- <template id="object"> -->
        <!--   <h1><t t-esc="object.display_name"/></h1> -->
        <!--   <dl> -->
        <!--     <t t-foreach="object._fields" t-as="field"> -->
        <!--       <dt><t t-esc="field"/></dt> -->
        <!--       <dd><t t-esc="object[field]"/></dd> -->
        <!--     </t> -->
        <!--   </dl> -->
        <!-- </template> -->
    </data>
</openerp>
```

Después de todo esto tendremos la base del Open Academy, a partir de ahora comenzaremos a añadir pestañas con diferentes funcionalidades:

Vamos a definir el modelo llamado Course. El curso tiene un titulo (obligatorio) y una descripción.

####models.py

```java
class Course(models.Model):
    _name = 'openacademy.course'

    name = fields.Char(string="Title", required=True)
    description = fields.Text()
Tambien tenemos que modificar el archivo xml demo.xml, añadiendo el siguiente <record>:

<record model="openacademy.course" id="course0">
            <field name="name">Course 0</field>
            <field name="description">Course 0's description

Can have multiple lines
            </field>
        </record>
        <record model="openacademy.course" id="course1">
            <field name="name">Course 1</field>
            <!-- no description for this one -->
        </record>
        <record model="openacademy.course" id="course2">
            <field name="name">Course 2</field>
            <field name="description">Course 2's description</field>
        </record>
```

Con esto hemos creado la pestaña **Courses** pero necesitamos algo para acceder a ella. A continuación:
- Implementaremos un botón para acceder .
- Añadiremos otro record para que podamos ver dentro de cada course el nombre y su descripción.
- Barra de búsqueda para poder buscar por título y descripción.

####openacademy.xml

```java
<?xml version="1.0" encoding="UTF-8"?>
<openerp>
    <data>
        <!-- window action -->
        <!--
            The following tag is an action definition for a "window action",
            that is an action opening a view or a set of views
        -->
        <record model="ir.actions.act_window" id="course_list_action">
            <field name="name">Courses</field>
            <field name="res_model">openacademy.course</field>
            <field name="view_type">form</field>
            <field name="view_mode">tree,form</field>
            <field name="help" type="html">
                <p class="oe_view_nocontent_create">Create the first course
                </p>
            </field>
        </record>

        <!-- top level menu: no parent -->
        <menuitem id="main_openacademy_menu" name="Open Academy"/>
        <!-- A first level in the left side menu is needed
             before using action= attribute -->
        <menuitem id="openacademy_menu" name="Open Academy"
                  parent="main_openacademy_menu"/>
        <!-- the following menuitem should appear *after*
             its parent openacademy_menu and *after* its
             action course_list_action -->
        <menuitem id="courses_menu" name="Courses" parent="openacademy_menu"
                  action="course_list_action"/>
        <!-- Full id location:
             action="openacademy.course_list_action"
             It is not required when it is the same module -->
    </data>
</openerp>
```

```java
<record model="ir.ui.view" id="course_form_view">
            <field name="name">course.form</field>
            <field name="model">openacademy.course</field>
            <field name="arch" type="xml">
                <form string="Course Form">
                    <sheet>
                        <group>
                            <field name="name"/>
                            <field name="description"/>
                        </group>
                    </sheet>
                </form>
            </field>
        </record>

<notebook>
           <page string="Description">
              <field name="description"/>
            </page>
            <page string="About">
              This is an example of notebooks
            </page>
</notebook>
```

####openerp.xml

```java
<record model="ir.ui.view" id="course_search_view">
            <field name="name">course.search</field>
            <field name="model">openacademy.course</field>
            <field name="arch" type="xml">
                <search>
                    <field name="name"/>
                    <field name="description"/>
                </search>
            </field>
</record>
```

##Creamos un modelo Session
Este modelo permitirá apuntarse a personas en los cursos y podrán elegir el día la duración y el numero de asientos. Para ello tendrá que escribir su nombre

####models.py

```java
class Session(models.Model):
    _name = 'openacademy.session'

    name = fields.Char(required=True)
    start_date = fields.Date()
    duration = fields.Float(digits=(6, 2), help="Duration in days")
    seats = fields.Integer(string="Number of seats")
```

####openacademy.xml

```java
<!-- session form view -->
        <record model="ir.ui.view" id="session_form_view">
            <field name="name">session.form</field>
            <field name="model">openacademy.session</field>
            <field name="arch" type="xml">
                <form string="Session Form">
                    <sheet>
                        <group>
                            <field name="name"/>
                            <field name="start_date"/>
                            <field name="duration"/>
                            <field name="seats"/>
                        </group>
                    </sheet>
                </form>
            </field>
        </record>

        <record model="ir.actions.act_window" id="session_list_action">
            <field name="name">Sessions</field>
            <field name="res_model">openacademy.session</field>
            <field name="view_type">form</field>
            <field name="view_mode">tree,form</field>
        </record>

        <menuitem id="session_menu" name="Sessions"
                  parent="openacademy_menu"
                  action="session_list_action"/>
```

Ahora crearemos relaciones **many2one**, **many2many** y **one2many** entre los **courses**, las **sessions** y los **attendees**.

**Many2One**
####models.py

```java
responsible_id = fields.Many2one('res.users',
        ondelete='set null', string="Responsible", index=True)

instructor_id = fields.Many2one('res.partner', string="Instructor")
    course_id = fields.Many2one('openacademy.course',
        ondelete='cascade', string="Course", required=True)
```

####openacademy.xml

```java
<field name="responsible_id"/>
```

**One2Many**

####models.py

```java
session_ids = fields.One2many(
        'openacademy.session', 'course_id', string="Sessions")
```

####openacademy.xml

```java
<page string="Sessions">
                                <field name="session_ids">
                                    <tree string="Registered sessions">
                                        <field name="name"/>
                                        <field name="instructor_id"/>
                                    </tree>
                                </field>
```

**Many2Many**

####models.py

```java
 attendee_ids = fields.Many2many('res.partner', string="Attendees")
```

####openacademy.xml

```java
<label for="attendee_ids"/>
<field name="attendee_ids"/>
```

##"EL TRAPO!!!"

##ONCHANGE

La siguiente parte de código no sirve para conseguir una advertencia cuando se introducen valores no válidos, como por ejemplo, un número nativo de asientos o más participantes que asientos.

####models.py

```java
@api.onchange('seats', 'attendee_ids')
    def _verify_valid_seats(self):
        if self.seats < 0:
            return {
                'warning': {
                    'title': "Incorrect 'seats' value",
                    'message': "The number of available seats may not be negative",
                },
            }
        if self.seats < len(self.attendee_ids):
            return {
                'warning': {
                    'title': "Too many attendees",
                    'message': "Increase seats or remove excess attendees",
                },
            }
```

##Constrains

De nuevo introduciremos código en Models.py, referente a restricciones, en este caso servirá para advertirnos si el instructor no está presente en los asientos de su propia sesión.

####models.py

```java
from openerp import models, fields, api, exceptions

@api.constrains('instructor_id', 'attendee_ids')
    def _check_instructor_not_in_attendees(self):
        for r in self:
            if r.instructor_id and r.instructor_id in r.attendee_ids:
                raise exceptions.ValidationError("A session's instructor can't be an attendee")
```

Continuamos en Models.py. En este caso se añadirá una limitación, la cual comprueba que la descripción del curso y el título del curso son diferentes, y también que el nombre del curso es único.

####models.py

```java
sql_constraints = [
        ('name_description_check',
         'CHECK(name != description)',
         "The title of the course should not be the description"),

        ('name_unique',
         'UNIQUE(name)',
         "The course title must be unique"),
    ]
```

Debido a lo introducido anteriormente se ha deshabilitado la posibilidad de utilizar la función “duplicar”, por ello debemos volver a implementarla (con el siguiente código):

####models.py

```java
@api.multi
    def copy(self, default=None):
        default = dict(default or {})

        copied_count = self.search_count(
            [('name', '=like', u"Copy of {}%".format(self.name))])
        if not copied_count:
            new_name = u"Copy of {}".format(self.name)
        else:
            new_name = u"Copy of {} ({})".format(self.name, copied_count)

        default['name'] = new_name
        return super(Course, self).copy(default)
```


##"EL TRAPO!!!"


##Advanced Views

En el siguiente paso, nos dedicaremos a darle formato a diferentes partes. Para la primera haremos una modificación en el apartado **Session** de tal forma que las sesiones que duren menos de cinco días serán de color azul , y las que duren más de quince días, de color rojo.

####openacademy.xml

```java
<tree string="Session Tree" decoration-info="duration&lt;5" decoration-danger="duration&gt;15">

<field name="duration" invisible="1"/>
```

Continuamos con la agregación de un calendario para el apartado **Session** que nos permitirá ver los eventos asociados a cada curso abierto.

####models.py

```java
from datetime import timedelta

end_date = fields.Date(string="End Date", store=True,
        compute='_get_end_date', inverse='_set_end_date')

@api.depends('start_date', 'duration')
    def _get_end_date(self):
        for r in self:
            if not (r.start_date and r.duration):
                r.end_date = r.start_date
                continue

            # Add duration to start_date, but: Monday + 5 days = Saturday, so
            # subtract one second to get on Friday instead
            start = fields.Datetime.from_string(r.start_date)
            duration = timedelta(days=r.duration, seconds=-1)
            r.end_date = start + duration

    def _set_end_date(self):
        for r in self:
            if not (r.start_date and r.end_date):
                continue

            # Compute the difference between dates, but: Friday - Monday = 4 days,
            # so add one day to get 5 days instead
            start_date = fields.Datetime.from_string(r.start_date)
            end_date = fields.Datetime.from_string(r.end_date)
            r.duration = (end_date - start_date).days + 1
```

####openacademy.xml

```java
<!-- calendar view -->
        <record model="ir.ui.view" id="session_calendar_view">
            <field name="name">session.calendar</field>
            <field name="model">openacademy.session</field>
            <field name="arch" type="xml">
                <calendar string="Session Calendar" date_start="start_date"
                          date_stop="end_date"
                          color="instructor_id">
                    <field name="name"/>
                </calendar>
            </field>
        </record>
```

Puntos de vista de la búsqueda, con esto nos referimos a añadir un botón para filtrar los cursos para los cuales el usuario actual es el responsable en la vista de búsqueda de cursos que se ha seleccionado por defecto.

####openacademy.xml

```java
<filter name="my_courses" string="My Courses"
                            domain="[('responsible_id', '=', uid)]"/>
                    <group string="Group By">
                        <filter name="by_responsible" string="Responsible"
                                context="{'group_by': 'responsible_id'}"/>
                    </group>
                    

<field name="context" eval="{'search_default_my_courses': 1}"/>

```

Lo siguiente que agregaremos serán los diagramas de **Gantt**, que permitirá al usuario ver la programación de sesiones relacionada con el módulo **openacademy**.

####models.py

```java
hours = fields.Float(string="Duration in hours",
                         compute='_get_hours', inverse='_set_hours')

@api.depends('duration')
    def _get_hours(self):
        for r in self:
            r.hours = r.duration * 24

    def _set_hours(self):
        for r in self:
            r.duration = r.hours / 24
```

####openacademy.xml

```java
<record model="ir.ui.view" id="session_gantt_view">
            <field name="name">session.gantt</field>
            <field name="model">openacademy.session</field>
            <field name="arch" type="xml">
                <gantt string="Session Gantt" color="course_id"
                       date_start="start_date" date_delay="hours"
                       default_group_by='instructor_id'>
                    <field name="name"/>
                </gantt>
            </field>
        </record>


<field name="view_mode">tree,form,calendar,gantt</field>
```

Para continuar, agregaremos una vista de gráficos en sesión que muestre, para cada curso, el número de asistentes bajo la forma de un gráfico de barras.

####models.py

```java
attendees_count = fields.Integer(
        string="Attendees count", compute='_get_attendees_count', store=True)

@api.depends('attendee_ids')
    def _get_attendees_count(self):
        for r in self:
            r.attendees_count = len(r.attendee_ids)
```

####openacademy.xml

```java
<record model="ir.ui.view" id="openacademy_session_graph_view">
            <field name="name">openacademy.session.graph</field>
            <field name="model">openacademy.session</field>
            <field name="arch" type="xml">
                <graph string="Participations by Courses">
                    <field name="course_id"/>
                    <field name="attendees_count" type="measure"/>
                </graph>
            </field>
        </record>
        
<field name="view_mode">tree,form,calendar,gantt,graph</field>
```

Por último, en este tutorial añadiremos la vista **Kanba**, una vista que muestra las sesiones agrupadas por columnas.

####models.py

```java
color = fields.Integer()
```

####openacademy.xml

```java
<record model="ir.ui.view" id="view_openacad_session_kanban">
            <field name="name">openacad.session.kanban</field>
            <field name="model">openacademy.session</field>
            <field name="arch" type="xml">
                <kanban default_group_by="course_id">
                    <field name="color"/>
                    <templates>
                        <t t-name="kanban-box">
                            <div
                                    t-attf-class="oe_kanban_color_{{kanban_getcolor(record.color.raw_value)}}
                                                  oe_kanban_global_click_edit oe_semantic_html_override
                                                  oe_kanban_card {{record.group_fancy==1 ? 'oe_kanban_card_fancy' : ''}}">
                                <div class="oe_dropdown_kanban">
                                    <!-- dropdown menu -->
                                    <div class="oe_dropdown_toggle">
                                        <i class="fa fa-bars fa-lg"/>
                                        <ul class="oe_dropdown_menu">
                                            <li>
                                                <a type="delete">Delete</a>
                                            </li>
                                            <li>
                                                <ul class="oe_kanban_colorpicker"
                                                    data-field="color"/>
                                            </li>
                                        </ul>
                                    </div>
                                    <div class="oe_clear"></div>
                                </div>
                                <div t-attf-class="oe_kanban_content">
                                    <!-- title -->
                                    Session name:
                                    <field name="name"/>
                                    <br/>
                                    Start date:
                                    <field name="start_date"/>
                                    <br/>
                                    duration:
                                    <field name="duration"/>
                                </div>
                            </div>
                        </t>
                    </templates>
                </kanban>
            </field>
        </record>
        
<field name="view_mode">tree,form,calendar,gantt,graph,kanban</field>
```

##"EL TRAPO!!!"
