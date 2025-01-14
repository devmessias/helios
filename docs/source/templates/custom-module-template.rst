{{ fullname | escape | underline}}


.. automodule:: {{ fullname }}
   

   {% block functions %}
   {% if functions %}
   .. rubric:: {{ _('Functions') }}

   .. autosummary::
      :toctree:
      :nosignatures:
   {% for item in functions %}
   .. autofunction:: {{ item }}

   .. _sphx_glr_backref_{{fullname}}.{{item}}:

   .. minigallery:: {{fullname}}.{{item}}
      :add-heading:

   {%- endfor %}
   {% endif %}
   {% endblock %}

   {% block classes %}
   {% if classes %}
   .. rubric:: {{ _('Classes') }}

  
   {% for objname in classes %}
   .. autoclass:: {{ objname }}
      :members:
      :show-inheritance:
      :inherited-members:
      :special-members: __call__, __add__, __mul__
      {% block methods %}
         {% if methods %}
         .. rubric:: {{ _('Methods') }}
         .. autosummary::
            :nosignatures:
         {% for item in methods %}
            {%- if not item.startswith('_') %}
            ~{{ name }}.{{ item }}
            {%- endif -%}
         {%- endfor %}
         {% endif %}
      {% endblock %}
      {% block attributes %}
         {% if attributes %}
         .. rubric:: {{ _('Class Attributes') }}
         .. autosummary::
         {% for item in attributes %}
            ~{{ name }}.{{ item }}
         {%- endfor %}
         {% endif %}
      {% endblock %}
      {% if objname=='MDE' or objname=='HeliosFr' or objname=='ForceAtlas2' %} 
      .. _sphx_glr_backref_helios.layouts.{{objname}}:
      .. minigallery:: helios.layouts.{{objname}}
         :add-heading:
      {% elif objname %}
      .. _sphx_glr_backref_{{fullname}}.{{objname}}:
      .. minigallery:: {{fullname}}.{{objname}}
         :add-heading:
      {% endif %}
   {%- endfor %}
   {% endif %}
   {% endblock %}

   {% block exceptions %}
   {% if exceptions %}
   .. rubric:: {{ _('Exceptions') }}

   .. autosummary::
      :toctree:
   {% for item in exceptions %}
      {{ item }}
   {%- endfor %}
   {% endif %}
   {% endblock %}

{% block modules %}
{% if modules %}
.. autosummary::
   :toctree:
   :template: custom-module-template.rst
   :recursive:
{% for item in modules %}
   {{ item }}
{%- endfor %}
{% endif %}
{% endblock %}