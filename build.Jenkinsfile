def xmlText = '''
<schemas>
 <schema name="lgstcs">
  <database name="deva">
   <property name="system">bid</property>
   <property name="name">devadwh</property>
   <property name="user">devadwh</property>
   <property name="pass">Devadwh123</property>
   <property name="host">dev01-tky-bidwh-ariake2-fr.clscmzfgj3i3.ap-northeast-1.redshift.amazonaws.com</property>
   <property name="port">5439</property>
   <property name="pack">dwh</property>
   <property name="dbmainuser"></property>
  </database>
 </schema>
 <schema name="iflgstcs">
  <database name="rela">
   <property name="system">bid</property>
   <property name="name">reladwh</property>
   <property name="user">reladwh</property>
   <property name="pass">Reladwh123</property>
   <property name="host">rel01-tky-bidwh-ariake2-fr.clscmzfgj3i3.ap-northeast-1.redshift.amazonaws.com</property>
   <property name="port">5439</property>
   <property name="pack">dwh</property>
   <property name="dbmainuser"></property>
  </database>
 </schema>
</schemas>
  '''
  
pipeline {
  agent any
  
  stages {
    stage('Stage 1') {
        steps {
            echo "${xmlText}"
            getDbProperties(xmlText)
        }
    }
  }
}

def getDbProperties(xmlString) {
  echo 'calling getDbProperties'
    def arrProperties = [:]
    
    try {
    def groovy.util.Node schemas = new XmlParser().parseText(xmlString)
    
    schemas.each { schema ->
        def schemaName = schema.@name
        arrProperties[schemaName] = [:]
        echo schemaName
        
        def groovy.util.Node dbs = schema.database
        dbs.each { db ->
            
                def dbName = db.@name
                echo dbName
                if ( dbName != null && dbName != "" ) {
                    arrProperties[schemaName][dbName] = db.text()
                }
            
        }
        
    }
    } catch ( e ) {
       echo e
    }
    
    return arrProperties
}
