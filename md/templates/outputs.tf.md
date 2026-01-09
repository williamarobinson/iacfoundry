output "{full_name}_output" {
  value = { for key, value in {full_name}.{resource} : key => value }
}

{if_has_name}
output "{full_name}_output_names" {
  value = { for key, value in {full_name}.{resource} : value.{key_attr} => value }
}
{endif_has_name}
